<template>
  <div class="searchWrapper">
    <input
      type="text"
      name="search"
      :value="value"
      @input="handleChange"
    />
  </div>
</template>

<script>
export default {
  name: 'Searchimput',
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style>
    .searchWrapper {
      display: flex;
      flex-direction: column;
      width: 250px;
    }
    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid #aaa;
      margin-top: 30px;
      background: none;
      color: #fff;
      text-align: center;
      font-size: 20px;
      transition: box-shadow .5s;
    }
    input:focus {
      outline: none;
      box-shadow: 0 5px 10px -8px #aaa;
    }
</style>
