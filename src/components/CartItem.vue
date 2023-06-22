<template>
    <div class="flex mb-6">
        <img :src="require(`@/images/${product.product.thumbnail}`)" class="h-12 mr-4" alt="">
        <div class="text-Dark-grayish-blue">
            <div>
                {{ product.product.name }}
            </div>
            <div>
                <span class="mr-2" >${{ product.product.price.afterDiscount.toFixed(2) }} × {{ product.count }}</span><span class="text-Very-dark-blue font-bold">${{ (product.product.price.afterDiscount*product.count).toFixed(2) }}</span>
            </div>
        </div>
        <button @click="clickDeleteItem" class="ml-auto">
            <img src="../images/icon-delete.svg" alt="">
        </button>
    </div>
</template>
<script>
export default {
    props: ['product'],
    methods: {
        clickDeleteItem(){
            this.$emit('onClickDeleteItem', this.product.product.id, this.product.count)
        }
    }
}
</script>
<style>
    
</style>