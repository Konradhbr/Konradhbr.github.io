<template>
  <div class="back">
    <img src="../assets/arrow.png" alt="" />
  </div>
</template>

<script>
export default {
  name: 'BackBtn',
};
</script>

<style lang="scss" scoped>
    .back {
      display: none;
      position: absolute;
      width: 40px;
      height: auto;
      left: 3%;
      cursor: pointer;

      img {
        width: 20px;
      }

      @media (min-width: 375px) {
        display: inherit;
      }

      @media (min-width: 1300px) {
        img {
          width: 40px;
        }
      }
    }
</style>
