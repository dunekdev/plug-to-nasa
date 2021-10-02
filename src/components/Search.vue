<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input
       type="text"
       name="search"
       id="search"
       v-model="searchValue"
       @input="handleClick"
       />
       <ul>
         <li v-for="item in results" :key="item.data[0].nasa_id">
           {{ item.data[0].description }}
         </li>
       </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';
export default {
  name: 'Search',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line
    handleClick: debounce(function () {
      axios.get(`${API}?q=${this.searchValue}&media_type=image`).then((response) => {
        this.results = response.data.collection.items;
      }).catch((error) => {
        console.log(error);
      });
    }, 500),
  },
};
</script>

<style scoped lang="scss">
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    box-sizing: border-box;
  }

  .search {
    display: flex;
    flex-direction: column;
    width: 300px;
    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
    }
    label {
      font-family: Arial, Helvetica, sans-serif;
    }
  }

</style>
