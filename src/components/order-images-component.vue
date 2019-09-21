<template>
  <div class="img-wrapper">
    <img :src="images.thumbnail"/>
  </div>
</template>

<script>
  export default {
    name: 'order-images-component',
    props: {
      images: Object
    }
  }
</script>

<style>
  .img-wrapper {
    position: relative;
    overflow: hidden;
    width: 100%;
    height: 116px;
  }

  .img-wrapper img {
    display: block;
    position: absolute;
    height: auto;
    width: 100%;
    top: -33px;
    left: 50%;
    transform: translateX(-50%);
  }

</style>