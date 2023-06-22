<template>
    <AppHeader @onClickMenuButton="onClickMenuButton" @onClickCartButton="onClickCartButton" :cartCount="cartTotalCount"/>
    <NavMenu v-if="isNavMenuOpen" @onClickCloseButton="onClickCloseButton"/>
    <CartBox class="transition-opacity hidden opacity-0" @onClickOutsideCartBox="onClickCartButton" :cartTotalCount="cartTotalCount" :products="cartProducts" @onClickDeleteItem="onClickDeleteItem"/>
    <ProductPage @onClickCarouselImage="onClickCarouselImage" @onAddToCart="onAddToCart" />
    <ProductImageCarouselFull class="transition-opacity hidden opacity-0" @onClickCloseButton="onClickCloseCarouselButton"/>
    
</template>

<script>
import NavMenu from './components/NavMenu.vue';
import AppHeader from './components/AppHeader.vue'
import CartBox from './components/CartBox.vue';
import ProductPage from './components/ProductPage.vue';
import ProductImageCarouselFull from './components/ProductImageCarouselFull.vue';

export default {
    name: 'App',
    components: {
    NavMenu,
    AppHeader,
    CartBox,
    ProductPage,
    ProductImageCarouselFull,
},
    data(){
        return {
            isNavMenuOpen: false,
            isCartBoxOpen: false,
            isProductCarouselOpen: false,
            cartProducts: [],
            cartTotalCount: 0
        }
    },
    watch: {
        isCartBoxOpen(newValue){
            let cartBoxEl = document.getElementById("cartBox")
            if(newValue===true){
                cartBoxEl.classList.remove('hidden')
                setTimeout(()=>{
                    cartBoxEl.classList.remove('opacity-0')
                },1)
            }
            else{
                cartBoxEl.classList.add('opacity-0')
                setTimeout(()=>{
                    cartBoxEl.classList.add('hidden')
                },100)
            }
        },
        isProductCarouselOpen(newValue){
            let productCarouselFull = document.getElementById('productCarouselFull')
            if(newValue===true){
                productCarouselFull.classList.remove('hidden')
                setTimeout(()=>{
                    productCarouselFull.classList.remove('opacity-0')
                },1)
            }
            else{
                productCarouselFull.classList.add('opacity-0')
                setTimeout(()=>{
                    productCarouselFull.classList.add('hidden')
                },100)
            }
        }
    },
    methods: {
        onClickMenuButton(){
            this.isNavMenuOpen = true
        },
        onClickCloseButton(){
            this.isNavMenuOpen = false
        },
        onClickCartButton(){
            this.isCartBoxOpen = !this.isCartBoxOpen
        },
        onAddToCart( product, count ){
            if (count>0){

                let sameProduct = this.cartProducts.find((x, i) => {
                    if (x.product.id === product.id){
                        this.cartProducts[i].count += count
                        return true
                    }
                })
                if (!sameProduct)
                    this.cartProducts.push( { product, count })
                this.cartTotalCount += count
                this.isCartBoxOpen = true
            }
        },
        onClickDeleteItem(id, count){
            this.cartProducts.find((x, i) => {
                if (x.product.id === id){
                    this.cartProducts.splice(i,1)
                }
            })
            this.cartTotalCount -= count
        },
        onClickCloseCarouselButton(){
            this.isProductCarouselOpen = false
        },
        onClickCarouselImage(){
            this.isProductCarouselOpen = true
        }
        
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap');
html, body, #app {
    @apply
        h-full
        bg-White
}
#app {
    @apply
        text-Very-dark-blue
        relative
        lg:px-40
}
</style>
