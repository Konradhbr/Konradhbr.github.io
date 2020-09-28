<template>
    <div class="backgroundImage"/>
</template>

<script>
export default {
  name: 'BackgroundImage',
};
</script>

<style lang="scss" scoped>

  .backgroundImage {
    position: fixed;
    width: 100%;
    height: 100vh;
    top: 0;
    z-index: -1;
    background-image: url('../assets/background.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 80% 0%;
  }
</style>
