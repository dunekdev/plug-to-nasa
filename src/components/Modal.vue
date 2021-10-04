<template>
    <div class="outerwrapper">
        <div class="innerwrapper">
            <div class="photo" :style="style"></div>
            <div class="desc">
                <h2 class="title">{{ item.data[0].title }}</h2>
                <p class="desc">{{ item.data[0].description }}</p>
            </div>
        </div>
        <div class="close" @click="$emit('closeModal')"></div>
    </div>
</template>
<script>
export default {
  name: 'Modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  computed: {
    style() {
      return `background-image: url("${this.item.links[0].href}")`;
    },
  },
};

</script>
<style lang="scss" scoped>
    .outerwrapper {
        max-width: 100%;
        position: fixed;
        top: 0;
        background: #fff;
        height: 100%;
        bottom: 0;
    }

    .close {
        position: absolute;
        top: 10px;
        right: 10px;
        background: #000;
        width: 20px;
        height: 20px;
    }

    .innerwrapper {
        display: flex;
        height: 100%;
        flex-direction: column;
        padding: 10px;
        justify-content: center;
        align-items: center;
    }

    .photo {
        width: 200px;
        height: 200px;
    }
</style>
