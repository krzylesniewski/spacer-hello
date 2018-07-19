<template>
  <div class="searchWrapper">
    <input
      type="text"
      name="search"
      :class="{ dark: dark }"
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
    .dark {
      color: #1e3d4a;
      border-bottom-color: #1e3d4a;
    }
    .dark:focus {
      outline: none;
      box-shadow: 0 10px 20px -8px rgba(#1e3d4a, .5);
    }
</style>
