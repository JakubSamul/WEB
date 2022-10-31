<template>
    <div class="searchWrapper">
      <input id="search" name="search" v-model="searchVolve" @input="handleInput" />
  </div>
</template>

<script>
export default {
  name: 'SearchImput',
};
</script>

<style lang="scss" scoped>
  .searchWrapper {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 250px;

    input {
      height: 30px;
      border: 0;
      background: none;
      border-bottom: 1px solid white;
    }
  }
</style>
