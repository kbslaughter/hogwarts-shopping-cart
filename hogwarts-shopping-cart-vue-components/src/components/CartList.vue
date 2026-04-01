<template>
    <div>
        <CartListItem v-for="cartItem in cartItems" :key="cartItem.id" :item="cartItem" @item-remove="$emit('item-remove', $event)"></CartListItem>
    </div>
</template>

<script setup>
import CartListItem from '@/components/CartListItem.vue';
defineProps(['cartItems'])
defineEmits(['item-remove', 'quantity-update'])

</script>

<style scoped></style>