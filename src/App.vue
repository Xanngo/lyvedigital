<template>
  <div id="app">
    <b-button @click="onShowModal">Show Order Modal</b-button>
    <order-component
      :order="order"
      :visible="showModal"
      @submit-budget="onBudgetSubmitted"
      @close="onModalClosed"
    ></order-component>
  </div>
</template>

<script>
import OrderComponent from './components/order-component.vue';


export default {
  name: 'app',
  components: {
    OrderComponent,
  },
  data() {
    return {
      showModal: false,
      order: {
        "order_description":{
          "id":22,
          "name":"10 healthy fruits you should eat",
          "publication":"healthyfruits.com",
          "before_submit_price":null,
          "description":"Enter the details of the article you want to order",
          "full_description":"Enter the details of the article you want to order",
          "order":1
        },
        "images":{
          "full_size":"https://upload.wikimedia.org/wikipedia/commons/2/2f/Culinary_fruits_front_view.jpg",
          "thumbnail":"https://upload.wikimedia.org/wikipedia/commons/thumb/2/2f/Culinary_fruits_front_view.jpg/440px-Culinary_fruits_front_view.jpg"
        },
        "Order_details":[
          {
             "id":24,
             "name":"source",
             "placeholder":"enter a link"
          },
          {
             "id":25,
             "name":"instructions",
             "placeholder":"enter your instructions"
          },
          {
             "id":26,
             "name":"number_writers",
             "placeholder":"select"
          },
          {
             "id":27,
             "name":"budget",
             "placeholder":"budget in USD"
          }
        ],
        "options":[
          {
             "id":222,
             "name":"Bilingual",
             "extra_id":2222,
             "increase":"20"
          },
          {
             "id":223,
             "name":"Copy-Editing",
             "extra_id":2223,
             "increase":"10"
          },
          {
             "id":224,
             "name":"Proof-reading",
             "extra_id":2224,
             "price":"20"
          }
        ]
      }
    }
  },
  methods: {
    onShowModal() {
      this.showModal = true;
    },
    onModalClosed() {
      this.showModal = false;
    },
    onBudgetSubmitted(totalBudget) {
      alert("Total Budget: " + totalBudget);
    }
  }
}
</script>

<style>
#app {
}

</style>
