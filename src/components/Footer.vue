<template>
  <div class="footerWrapper">
      <footer>Powered by Pixabay</footer>
  </div>
</template>

<script>
export default {
    name: 'footer',
};
</script>

<style lang="scss" scoped>

    footer {
        display: flex;
        justify-content: center;
        position: relative;
        bottom: -24vh;
        font-size: 13px;
        font-weight: 400;
        color: white;

        @media (min-width: 768px) {
            font-size: 17px;
            width: 500px;
            letter-spacing: 1px;
            line-height: 1;
    }
    }
</style>