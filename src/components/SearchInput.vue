<template>
    <div class="search">
        <input
        type="text"
        name="search"
        :class="{ dark }"
        :value="value"
        @input="handleChange"
        autofocus
        />
    </div>
</template>
<script>

export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};

</script>
<style lang="scss" scoped>
    .search {
        display: flex;
        flex-direction: column;
        width: 300px;
        margin-bottom: 20px;
        input {
            height: 30px;
            border: 0;
            border-bottom: 1px solid black;
            text-align: center;
          &.dark {
            border-bottom: 1px solid red;
          }
          &:focus {
            outline: none;
          }
        }
    }

</style>
