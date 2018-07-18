<template>
  <div class="wrapper">
      <Claim />
      <Searchimput />
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import Searchimput from '@/components/Searchimput.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Home',
  components: {
    Claim,
    Searchimput,
  },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
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
        background-image: url('../assets/discovery-launch-liftoff-23764.jpg');
        background-repeat: no-repeat;
        background-size: cover;
        background-position: 30% 0%;
    }
</style>
