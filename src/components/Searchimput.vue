<template>
  <div class="searchWrapper">
    <input
      type="text"
      name="search"
      v-model="searchValue"
      @input="handleInput"
    />
  </div>
</template>

<script>
export default {
  name: 'Searchimput.vue',
};
</script>

<style>
    .searchWrapper{
      display: flex;
      flex-direction: column;
      width: 250px;
    }
    input{
      height: 30px;
      border: 0;
      border-bottom: 1px solid #aaa;
      margin-top: 30px;
      background: none;
      color: #fff;
      text-align: center;
    }
</style>
