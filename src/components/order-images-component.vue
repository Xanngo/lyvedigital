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
    height: 156%;
    top: -33px;
  }
</style>