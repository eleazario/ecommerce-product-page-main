<template>
    <main class="z-0 lg:py-[5.5rem] lg:px-14 lg:flex">
        <div class="carousel lg:w-[27.75rem]">
            <!-- sm -->
            <Flicking ref="flicking" class="lg:hidden" :options="flickingOptions">
                <img v-for="x in 4" :key="x" :src="require(`../images/image-product-${x}.jpg`)" class="productImage" alt="">
            </Flicking>
            <!--  -->
            <!-- lg -->
            <Flicking @click="clickCarouselImage" ref="flickingLg" class="hidden lg:block w-[27.75rem] rounded-2xl cursor-pointer" :options="flickingOptionsLg">
                <img v-for="x in 4" :key="x" :src="require(`../images/image-product-${x}.jpg`)" class="productImage" alt="">
            </Flicking>
            <!--  -->
            <button @click="carouselPrev" class="left-0 ml-4"><img src="../images/icon-previous.svg" alt=""></button>
            <button @click="carouselNext" class="right-0 mr-4"><img src="../images/icon-next.svg" alt=""></button>

            <div class="hidden lg:grid grid-cols-4 gap-7 mt-7">
                <ProductThumbnail 
                    v-for="x in 4"
                    :key="x"
                    :productNumber="x"
                    @onProductThumbnailClick="onProductThumbnailClick(x)"
                    :flickingIndex="flickingIndex"
                />
            </div>
        </div>
        <div class="px-6 pt-5 pb-16 lg:p-0 lg:pt-14 lg:pl-32 lg:w-auto">
            <div class="mb-3 text-sm font-bold text-Orange lg:tracking-widest">
                SNEAKER COMPANY
            </div>
            <div class="mb-4 lg:mb-9 text-3xl lg:text-[2.65rem] font-bold text-Very-dark-blue lg:leading-[3rem]">
                {{ product.name }}
            </div>
            <p class="mb-7 lg:mb-6 text-Dark-grayish-blue leading-[1.6rem]">
                {{ product.description }}
            </p>
            <div class="flex mb-3 lg:mb-1 items-center">
                <div class="text-3xl font-bold text-Very-dark-blue mr-4">
                    ${{ product.price.afterDiscount.toFixed(2) }}
                </div>
                <div class="flex font-bold text-lg h-8 w-14 rounded-lg items-center text-Orange bg-Pale-orange">
                    <span class="mx-auto">
                        {{ product.price.discountPercent }}%
                    </span>
                </div>
                <div class="lg:hidden text-lg font-bold line-through text-Grayish-blue ml-auto">
                    ${{ product.price.normal.toFixed(2) }}
                </div>
            </div>
            <div class="hidden lg:block mb-8 text-lg font-bold line-through text-Grayish-blue ml-auto">
                    ${{ product.price.normal.toFixed(2) }}
                </div>
            <div class="lg:flex">
                <div class="productCountBox">
                    <button @click="minusCart" class="px-6 lg:px-3"><img src="../images/icon-minus.svg" alt=""></button>
                    <div class="flex items-center text-lg text-Very-dark-blue font-bold">{{ addToCartCount }}</div>
                    <button @click="plusCart" class="px-6 lg:px-3"><img src="../images/icon-plus.svg" alt=""></button>
                </div>
                <button @click="addToCart" class="addToCartButton">
                    <img class="h-[0.9rem]" src="../images/icon-cart-white.svg" alt="">
                    <span class="text-White font-bold">Add to cart</span>
                </button>
            </div>
        </div>
    </main>
</template>
<script>
import ProductThumbnail from "./ProductThumbnail.vue";
import Flicking from "@egjs/vue3-flicking";
import { FlickingError, ERROR_CODE } from "@egjs/flicking";
import "@egjs/vue3-flicking/dist/flicking.css"

export default {
    components: {
        Flicking,
        ProductThumbnail
    },
    data(){
        return {
            product: {
                id: 1,
                name: 'Fall Limited Edition Sneakers',
                thumbnail: 'image-product-1-thumbnail.jpg',
                description: "These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole, they'll withstand everything the weather can offer.",
                price: {
                    normal: 250.00,
                    discountPercent: 50,
                    afterDiscount: 125.00
                }
            },
            addToCartCount: 0,
            flickingIndex: null,
            flickingOptions: {
                renderOnlyVisible: true,
                circular: true
            },
            flickingOptionsLg: {
                renderOnlyVisible: true,
                disableOnInit: true,
                panelsPerView: 1,
                duration: 150
            }
        }
    },
    mounted(){
        this.flickingIndex = this.$refs.flickingLg.index
    },
    methods: {
        async carouselPrev(){
            try {
                await this.$refs.flicking.prev()
            } catch (error) {
                if (error instanceof FlickingError){
                    if (error.code === ERROR_CODE.ANIMATION_ALREADY_PLAYING) {
                        console.error("Animation is already playing!");
                    }
                    else if (error.code === ERROR_CODE.ANIMATION_INTERRUPTED) {
                        console.error("Animation is interrupted by user.");
                    }
                }
            }
        },

        async carouselNext(){
            try {
                await this.$refs.flicking.next()
            } catch (error) {
                if (error instanceof FlickingError){
                    if (error.code === ERROR_CODE.ANIMATION_ALREADY_PLAYING) {
                        console.error("Animation is already playing!");
                    }
                    else if (error.code === ERROR_CODE.ANIMATION_INTERRUPTED) {
                        console.error("Animation is interrupted by user.");
                    }
                }
            }
        },

        async onProductThumbnailClick(index){
            try {
                await this.$refs.flickingLg.moveTo(index-1)
                    .then(()=>{
                        this.flickingIndex = index-1
                    })
            } 
            catch (error) {
                console.log(error);
            }
        },

        minusCart(){
            if (this.addToCartCount>0)
                this.addToCartCount--
        },
        plusCart(){
            this.addToCartCount++
        },

        addToCart(){
            this.$emit('onAddToCart',  this.product, this.addToCartCount)
        },

        clickCarouselImage(){
            this.$emit('onClickCarouselImage')
        }
    }
}
</script>
<style>
.carousel {
    @apply
        relative
}

.carousel > button {
    @apply
        z-[5]
        absolute
        top-36
        h-10
        w-10
        bg-White
        rounded-full
        lg:hidden
}

.carousel > button > img {
    @apply
        mx-auto
}

.productImage {
    @apply
        object-cover
        w-full
        h-80
        lg:h-[27.75rem]
        lg:w-[27.75rem]        
}

button {
    @apply
        transition-opacity
}

.addToCartButton {
    @apply
        flex 
        gap-4
        w-full 
        h-14 
        items-center 
        justify-center 
        rounded-xl 
        bg-Orange 
        shadow-Pale-orange 
        shadow-2xl
        hover:opacity-60
}

.productCountBox {
    @apply
    flex 
    h-14
    w-full 
    lg:w-60 
    mb-4 
    lg:mr-4 
    justify-between
    bg-Light-grayish-blue 
    rounded-xl
}

.productCountBox > button {
    @apply
        hover:opacity-60
}
</style>