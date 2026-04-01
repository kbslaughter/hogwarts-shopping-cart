<template>
    <div>
        <CartTitle :username="username"></CartTitle>
        <div class="cart-container">
            <CartList 
              class="cart-list" 
              :cart-items="shoppingCartItems" 
              @item-remove="removeItem($event)" 
              @quantity-update="updateQuantity($event)"
            ></CartList>
            <OrderSummary class="order-summary" :cart-items="shoppingCartItems"></OrderSummary>
        </div>
    </div>
</template>

<script setup>
import CartList from '@/components/CartList.vue';
import CartTitle from '@/components/CartTitle.vue';
import OrderSummary from '@/components/OrderSummary.vue';
import { ref, watch } from 'vue';

let username = ref('Harry Potter');
let shoppingCartItems = ref([
    {
      id: 1,
      name: 'Dragon Liver',
      price: 1500,
      quantity: 3,
      inStock: true,
      image: 'src/assets/img/DragonLiver.png',
    },
    {
      id: 2,
      name: 'Golden Snitch',
      price: 600,
      quantity: 2,
      inStock: true,
      image: 'src/assets/img/GoldenSnitch.png',
    },
    {
      id: 3,
      name: 'Unicorn Tail Hair',
      price: 1200,
      quantity: 1,
      inStock: false,
      image: 'src/assets/img/UnicornTailHair.png',
    },
    {
      id: 4,
      name: 'Wand',
      price: 2000,
      quantity: 1,
      inStock: true,
      image: 'src/assets/img/Wand.jpg',
    },
    {
      id: 5,
      name: 'Nimbus 2000',
      price: 5000,
      quantity: 1,
      inStock: true,
      image: 'src/assets/img/Nimbus2000.png',
    },
  ])

  function removeItem(id) {
    let index = shoppingCartItems.value.findIndex(item => item.id == id);
    shoppingCartItems.value.splice(index, 1);
  }
 
  function updateQuantity(val) {
    const { id, newQuantity } = val;
    shoppingCartItems.value.some(item=>{
      if(item.id == id) {
        item.quantity = parseInt(newQuantity);
        return true;
      }
    })
  }

  watch(
    shoppingCartItems,
    () => {
      localStorage.setItem(
        'shoppingCartItems', 
        JSON.stringify(shoppingCartItems.value)
      )
    },
    { deep: true }
  )

</script>

<style scoped>
 /* Styles for the cart list and order summary */
  .cart-container {
    display: flex;
    align-items: flex-start;
    max-width: 1200px;
    margin: auto;
  }

  .cart-list {
    flex-grow: 2;
    margin-right: 20px;
  }

  .order-summary {
    flex-basis: 300px;
    background-color: #f9fafb;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

</style>