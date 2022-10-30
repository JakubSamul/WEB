<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search
        <input id="search" name="search" v-model="searchVolve" @input="handleInput" /></label>
    </div>
  </div>
</template>
<script>
import axios from 'axios';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'NasaSearch',
  data() {
    return {
      searchVolve: '',
    };
  },
  methods: {
    handleInput() {
      axios.get(`${API}?q=${this.searchVolve}&media_type=image`)
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
<style lang="scss" scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
  }

  .search {
    display: flex;
    flex-direction: column;
    width: 250px;

    label {
      font-family: Montserrat, sans-serif;
    }

    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid block;
    }
  }
</style>
