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
      <Modal v-if="modalOpen" @closeModal="modalOpen = false"/>
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
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
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

</style>
