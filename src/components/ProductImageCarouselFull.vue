<template>
    <div @click.self="clickCloseButton" id="productCarouselFull" class="fixed flex content-center top-0 z-20 -ml-40 w-full h-full bg-Black-transparent">
        
        <div class="w-fit mx-auto">
            <div class="flex">
                <button @click="clickCloseButton" class="buttonClose p-4 ml-auto mt-4 -mr-6">
                    <svg width="24" height="24" viewBox="0 0 18 18" xmlns="http://www.w3.org/2000/svg">
                        <path d="m11.596.782 2.122 2.122L9.12 7.499l4.597 4.597-2.122 2.122L7 9.62l-4.595 4.597-2.122-2.122L4.878 7.5.282 2.904 2.404.782l4.595 4.596L11.596.782Z" fill="hsl(0, 0%, 100%)" fill-rule="evenodd"/>
                    </svg>
                </button>
            </div>
            <div class="relative w-fit mx-auto">
                <Flicking ref="flicking" class="rounded-2xl m-auto w-[35rem]" :options="flickingOptions">
                    <img v-for="x in 4" :key="x" :src="require(`../images/image-product-${x}.jpg`)" class="productImage" alt="">
                </Flicking>
                <button @click="carouselPrev" class="carouselButtonNav left-0 -ml-6">
                    <svg width="12" height="18" xmlns="http://www.w3.org/2000/svg"><path d="M11 1 3 9l8 8" stroke="#1D2026" stroke-width="3" fill="none" fill-rule="evenodd"/></svg>
                </button>
                <button @click="carouselNext" class="carouselButtonNav right-0 -mr-6">
                    <svg width="13" height="18" xmlns="http://www.w3.org/2000/svg"><path d="m2 1 8 8-8 8" stroke="#1D2026" stroke-width="3" fill="none" fill-rule="evenodd"/></svg>
                </button>
            </div>
            <div class="grid grid-cols-4 gap-7 mx-auto mt-7 w-[28rem]">
                <ProductThumbnail 
                    v-for="x in 4"
                    :key="x"
                    :productNumber="x"
                    @onProductThumbnailClick="onProductThumbnailClick(x)"
                    :flickingIndex="flickingIndex"
                />
            </div>
        </div>
        
    </div>
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
            flickingIndex: 0,
            flickingOptions: {
                circular: true,
                renderOnlyVisible: true,
                disableOnInit: true,
                panelsPerView: 1,
                duration: 150
            }
        }
    },
    methods: {
        clickCloseButton(){
            this.$emit('onClickCloseButton')
        },

        async carouselPrev(){
            try {
                await this.$refs.flicking.prev()
                    .then(()=>{
                        this.flickingIndex = this.$refs.flicking.index
                    })
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
                    .then(()=>{
                        this.flickingIndex = this.$refs.flicking.index
                    })
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
                await this.$refs.flicking.moveTo(index-1)
                    .then(()=>{
                        this.flickingIndex = index-1
                    })
            } 
            catch (error) {
                console.log(error);
            }
        },
    }
}
</script>
<style scoped>
.buttonClose:hover > svg > path {
    @apply
        fill-Orange
}
.productImage {
    @apply
        object-cover
        w-full
        h-80
        lg:h-[35rem]
        lg:w-[35rem]        
}

button > svg > path {
    @apply
        transition-[stroke,fill]
}

.carouselButtonNav {
    @apply
        z-10
        absolute
        top-[16rem]
        h-[3.25rem]
        w-[3.25rem]
        bg-White
        rounded-full
}

.carouselButtonNav > svg {
    @apply
        mx-auto
}

.carouselButtonNav:hover > svg > path {
    @apply
        stroke-Orange
}
</style>