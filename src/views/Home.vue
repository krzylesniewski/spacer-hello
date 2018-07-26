<template>
  <div :class="[ {flexStart: step === 1} , 'wrapper']">
      <transition name="component-fade">
        <HeroImage v-if="step === 0" />
      </transition>
      <Claim v-if="step === 0" />
      <Searchimput v-model="searchValue" @input="handleInput" :dark="step === 1" />
      <!--  v-if="results && !loading && step === 1"  <-Tak powinno byc  -->
      <div class="results" v-if=" results">
        <Item v-for="item in results" :item="item"
            :key="item.data[0].nasa_id"
            @click.native="handleModalOpen(item)"/>
      </div>
      <div class="lds-default" v-if="step === 1 && loading">       <div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div>
      </div>
      <Modal v-if="modalOpen" :item="modalData" @closeModal="modalOpen = false"/>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import Searchimput from '@/components/Searchimput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Home',
  components: {
    Claim,
    Searchimput,
    HeroImage,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalData: false,
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalData = item;
      console.log(item);
    },
    handleInput: debounce(function () {
      this.loading = true; // reset status change for begignig of animation
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = true; // set status change for begignig of animation
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
    .wrapper {
        box-sizing: border-box;
        margin: 0 auto;
        height: 100vh;
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 30px;

        &.flexStart{
          justify-content: flex-start;
        }
    }
    .component-fade-enter-active, .component-fade-leave-active {
      transition: opacity .8s ease;
    }
    .component-fade-enter, .component-fade-leave-to {
      opacity: 0;
    }
    .results{
      margin: 0 auto;
      margin-top: 15px;
      width: 80%;
      display: grid;
      grid-template-columns: 1fr;
      grid-gap: 10px;
       @media (min-width: 480px) {
        grid-template-columns: 1fr 1fr;
      }
      @media (min-width: 768px) {
        grid-template-columns: 1fr 1fr 1fr;
      }
    }
.lds-default {
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
}
.lds-default div {
  position: absolute;
  width: 5px;
  height: 5px;
  background: #fff;
  border-radius: 50%;
  animation: lds-default 1.2s linear infinite;
}
.lds-default div:nth-child(1) {
  animation-delay: 0s;
  top: 29px;
  left: 53px;
}
.lds-default div:nth-child(2) {
  animation-delay: -0.1s;
  top: 18px;
  left: 50px;
}
.lds-default div:nth-child(3) {
  animation-delay: -0.2s;
  top: 9px;
  left: 41px;
}
.lds-default div:nth-child(4) {
  animation-delay: -0.3s;
  top: 6px;
  left: 29px;
}
.lds-default div:nth-child(5) {
  animation-delay: -0.4s;
  top: 9px;
  left: 18px;
}
.lds-default div:nth-child(6) {
  animation-delay: -0.5s;
  top: 18px;
  left: 9px;
}
.lds-default div:nth-child(7) {
  animation-delay: -0.6s;
  top: 29px;
  left: 6px;
}
.lds-default div:nth-child(8) {
  animation-delay: -0.7s;
  top: 41px;
  left: 9px;
}
.lds-default div:nth-child(9) {
  animation-delay: -0.8s;
  top: 50px;
  left: 18px;
}
.lds-default div:nth-child(10) {
  animation-delay: -0.9s;
  top: 53px;
  left: 29px;
}
.lds-default div:nth-child(11) {
  animation-delay: -1s;
  top: 50px;
  left: 41px;
}
.lds-default div:nth-child(12) {
  animation-delay: -1.1s;
  top: 41px;
  left: 50px;
}
@keyframes lds-default {
  0%, 20%, 80%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.5);
  }
}



</style>
