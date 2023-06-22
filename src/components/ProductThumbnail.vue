<template>
    <div :class="[{activeImageProduct: productNumber == flickingIndex+1}]" >
        <img 
            :src="require(`../images/image-product-${productNumber}-thumbnail.jpg`)" 
            @click="productThumbnailClick(productNumber)" 
            alt=""
        >
    </div>
</template>
<script>
export default {
    props: ['productNumber', 'flickingIndex'],
    methods: {
        productThumbnailClick(){
            this.$emit('onProductThumbnailClick', this.productNumber)
        }
    }
}
</script>
<style scoped>

div {
    @apply
        cursor-pointer
        rounded-lg
        hover:bg-White
        transition-[background-color,outline]
        outline
        outline-2
        outline-[hsla(0,0%,0%,0)]
}

img {
    @apply
        transition-opacity
        hover:opacity-50
        rounded-lg
}

.activeImageProduct {
    @apply
        bg-White
        outline-Orange
}

.activeImageProduct > img {
    @apply
        opacity-50
}

</style>