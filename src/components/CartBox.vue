<template>
    <div @click.self="clickOutsideCartBox" id="cartBox" class="fixed w-screen h-screen top-20 px-2 z-20 lg:-ml-40">
        <div class="bg-White rounded-lg shadow-Black-transparent-low shadow-xl lg:w-[22rem] lg:absolute lg:right-24">
            <div class="p-6 border-b-2 border-Light-grayish-blue font-bold">
                Cart
            </div>
            <div  v-if="cartTotalCount === 0" class="h-[184px] h text-center text-Dark-grayish-blue font-bold flex items-center">
                <div class="flex-auto">
                    Your cart is empty.
                </div>
            </div>
            <div v-else class="p-6">
                <CartItem @onClickDeleteItem="onClickDeleteItem" v-for="product in products" :key="product.id" :product="product" />
                <button class="mb-2 text-center text-White font-bold bg-Orange h-14 w-full rounded-xl">Checkout</button>
            </div>
        </div>
    </div>
</template>
<script>
import CartItem from './CartItem.vue';
export default {
    props: ['cartTotalCount', 'products'],
    components: {
        CartItem,
},
    methods: {
        clickOutsideCartBox(){
            this.$emit('onClickOutsideCartBox')
        },
        clickButtonDelete(){
            this.$emit('onClickButtonDelete')
        },
        onClickDeleteItem(id, count){
            this.$emit('onClickDeleteItem', id, count)
        }
    }
}
</script>
<style scoped>
button {
    @apply
        transition-opacity
        hover:opacity-60
}
</style>