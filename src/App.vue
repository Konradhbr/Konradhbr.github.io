<template>
    <div :class="[{flexStart: step===1} ,'wrapper']">
      <transition name="slide">
        <h1 class="logo" v-if="step===1">ImageWise</h1>
      </transition>
      <transition name="fade">
        <BackgroundImage v-if="step=== 0"/>
      </transition>
      <Claim v-if="step=== 0"/>
      <SearchInput v-model="searchValue" @input="handleInput" :dark="step===1"/>
      <Footer v-if="step=== 0"/> 
      <div class="results" v-if="results && !loading && step===1">
        <Item v-for="item in results" :item="item" :key="item.id" @click.native="handleModalOpen(item)"/>
      </div>
      <div class="loader" v-if="step===1 && loading" />
      <Modal v-if="modalOpen" :item="modalItem"  @closemodal="modalOpen=false" />
    </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import BackgroundImage from '@/components/BackgroundImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';
import Footer from '@/components/Footer.vue';


const API = 'https://pixabay.com/api/?key=18016858-8dfc07526ef2591a79bd76aea';
export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    BackgroundImage,
    Item,
    Modal,
    Footer,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}&q=${this.searchValue}&image_type=photo`)
        .then((response) => {
          this.results = response.data.hits;
          this.loading = false;
          this.step = 1;
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },

};
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800&display=swap');

@font-weight-light: 300;
@font-weight-normal: 400;
@font-weight-bold: 600;
@font-weight-block: 800;


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

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .3s ease;
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
  height: 100vh;
  min-height: 100vh;
  padding: 30px;
  width: 100%;
  justify-content: center;

    &.flexStart{
      justify-content: flex-start;
    }

  }
  .logo {
    position: absolute;
    top: 0px;
    font-family: 'Montserrat', sans-serif;
    letter-spacing: 2px;
    font-weight: 900;
  }

  .results {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-column-gap: 20px;
    grid-row-gap: 20px;

    @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
      grid-column-gap: 20px;
      grid-row-gap: 20px;
    }
  }


  .loader {
    margin-top: 100px;
    display: inline-block;
    width: 64px;
    height: 64px;

    @media (min-width: 768px) {
      width: 90px;
      height: 90px;
    }
  }
  .loader:after {
    content: " ";
    display: block;
    width: 46px;
    height: 46px;
    margin: 1px;
    border-radius: 50%;
    border: 5px solid #1e3d4a;
    border-color: #1e3d4a transparent #1e3d4a transparent;
    animation: loading 1.2s linear infinite;
  }
  @keyframes loading {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
}


</style>
