<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img src="./assets/logo.png" alt="description of image" class="logo" v-if="step === 1">
    </transition>
    <transition name="fond">
      <Background v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <SearchImput v-model="searchValue" @input="handleInput" :dark="step === 1" />
    <div class="reasults">
      <div v-for="item in reasults">
        <p>{{ item.links[0].href }}</p>
      </div>
    </div>
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
      loading: false,
      step: 0,
      searchVolve: '',
      results: [],
    };
  },
  methods: {
    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchVolve}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
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

.fond-enter-active, .fond-leave-active {
  transition: opacity 1s ease;
}

.fond-enter, .fond-leave-to {
  opacity: 0;
}

.slide-enter-active, .slide-leave-active {
  transition: margin-top 1s ease;
}

.slide-enter, .slide-leave-to {
  margin-top: -50px;
}

.wrapper {
  display: flex;
  position: relative;
  flex-direction: column;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  min-height: 100vh;
  justify-content: center;

  &.flexStart {
    justify-content: flex-start;
  }
}

.logo {
  position: absolute;
  top: 40px;
}
</style>
