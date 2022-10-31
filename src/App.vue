<template>
  <div class="wrapper">
    <Background />
    <Claim />
    <SearchImput v-model="searchValue" @input="handleInput" />
  </div>
</template>
<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchImput from '@/components/SearchImput.vue';
import Background from '@/components/Background.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',
  components: {
    Background,
    Claim,
    SearchImput,
  },
  data() {
    return {
      searchVolve: '',
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchVolve}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200;400;600;800&display=swap');

* {
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font-family: 'Montserrat', sans-serif;
  margin: 0;
  padding: 0;
}

.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  min-height: 100vh;
  justify-content: center;
}
</style>
