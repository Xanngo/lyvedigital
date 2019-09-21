
<template>
  <div class="order-component">
    <div class="order-modal">
      <div class="order-wrapper">
        <header>
          <order-images-component :images="order.images"/>
          <button class="bo-back">
            <i class="fas fa-arrow-left" aria-hidden="true"></i>
          </button>
          <order-description-component :order-description="order.order_description"/>
        </header>
        <order-form-component :order-details="order.Order_details" :options="order.options"/>
      </div>
    </div>
  </div>
</template>

<script>
  import OrderImagesComponent from './order-images-component.vue';
  import OrderDescriptionComponent from './order-description-component.vue';
  import OrderFormComponent from './order-form-component.vue';

  export default {
    name: 'order-component',
    components: {
      OrderImagesComponent,
      OrderDescriptionComponent,
      OrderFormComponent,
    },
    props: {
      order: Object
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Roboto:300,500,700,900&display=swap');

  .order-component {
    width: 100vw;
    height: 100vh;
    min-width: 271px;
    min-height: 641px;
    font-family: 'Roboto', sans-serif;
    font-size: 16px;
  }
  .order-component .order-modal {
    position: relative;
    height: 100%;
    width: 100%;
    background-color: #FFFFFF;
  }

  .order-component .order-modal .order-wrapper {
    position: absolute;
    top: 10px;
    left: 0;
    right: 0;
    bottom: 10px;
    border-bottom: 1px solid #ececec;
  }

  .order-component header {
    border-bottom: 1px solid #f1f1f1;
    position: relative;
  }

  .order-component header .bo-back {
    position: absolute;
    top: 10px;
    left: 6px;
    height: 34px;
    width: 34px;
    border: none;
    border-radius: 100%;
    background-color: #fdfdfd;
    color: #aeaeae;
  }

  .order-component header .container {
    padding: 9px 7px;
    padding-bottom: 5px;
  }

  .order-component .title {
    font-weight: 900;
    font-size: 0.8em;
    letter-spacing: 0.5px;
  }
  .order-component .home {
    font-size: 0.55em;
    margin-top: 3px;
  }
  .order-component .home a {
    color: #57e8bb;
    background-color: #f6f9fa;
    padding: 2px 3px;
    border-radius: 2px;
  }
  
  .order-component .description {
    font-size: 0.59em;
    margin-top: 10px;
    color: #2b5da9;
  }

  @media (min-height: 700px) {
    .order-component {
      font-size: 18px;
      background-color: rgba(0,0,0,0.5);
    }
    .order-component .order-modal {
      max-width: 500px;
      max-height: 700px;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      border: 3px solid #2c68c1;
      border-radius: 13px;
    }
  }
</style>
