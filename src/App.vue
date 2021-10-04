<template>
  <div class="app">
    <div class="wrapper">
      <transition name="slide-fade">
        <img v-if="step === 1" src="./assets/logo.png" class="logo" alt="logo">
      </transition>
      <transition name="fade">
        <Claim v-if="step === 0" />
      </transition>
      <SearchInput
      v-model="searchValue"
      :dark="step === 1"
      @input="handleClick"
      />
      <div class="results">
        <Item
        v-for="item in results"
        :item="item" :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
        />
      </div>
      <div class="loader" v-if="step === 1 && loading"></div>
      <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';
export default {
  name: 'App',
  data() {
    return {
      searchValue: '',
      results: [],
      loading: false,
      modalItem: null,
      step: 0,
      modalOpen: false,
    };
  },
  components: {
    Claim,
    SearchInput,
    Item,
    Modal,
  },
  methods: {
    // eslint-disable-next-line
    handleClick: debounce(function () {
      this.loading = true;
      this.results = [];
      axios.get(`${API}?q=${this.searchValue}&media_type=image`).then((response) => {
        this.results = response.data.collection.items;
        this.loading = false;
        this.step = 1;
      }).catch((error) => {
        console.log(error);
      });
    }, 500),
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
  },
};
</script>

<style scoped lang="scss">
  * {
    box-sizing: border-box;
  }
  .wrapper {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
  }

  .logo {
    position: absolute;
    top: 0;
    width: 40px;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }
  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }

  .slide-fade-enter-active {
    transition: all .3s ease;
    transition-delay: 1s;
  }
  .slide-fade-leave-active {
    transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .slide-fade-enter, .slide-fade-leave-to
  /* .slide-fade-leave-active below version 2.1.8 */ {
    transform: translateY(-10px);
    opacity: 0;
  }

  .results {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }

.loader {
  display: inline-block;
  width: 80px;
  height: 80px;
}
.loader:after {
  content: "";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #000;
  border-color: #000 transparent #000 transparent;
  animation: loader 1.2s linear infinite;
}
@keyframes loader {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

</style>
