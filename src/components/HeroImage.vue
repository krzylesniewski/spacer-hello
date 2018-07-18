<template>
    <div class="heroImage"></div>
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style>
  .heroImage{
        position: fixed;
        z-index: -1;
        width: 100%;
        height: 100vh;
        min-height: 100vh;
        background-image: url('../assets/discovery-launch-liftoff-23764.jpg');
        background-repeat: no-repeat;
        background-size: cover;
        background-position: 30% 0%;
  }
</style>
