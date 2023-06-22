<template>
    <div @click.self="clickCloseButton" class="h-full w-full fixed top-0 bg-Black-transparent z-30">
        <div id="nav" class="bg-White h-full w-[15.5rem] p-6">
            <button @click="clickCloseButton" class="mb-12">
                <img src="../images/icon-close.svg" alt="">
            </button>
            <nav class="flex flex-col text-lg font-bold gap-[1.15rem]">
                <a href="">Collections</a>
                <a href="">Men</a>
                <a href="">Women</a>
                <a href="">About</a>
                <a href="">Contact</a>
            </nav>
        </div>
    </div>
</template>
<script>

export default {
    methods: {
        clickCloseButton(){
            this.$emit('onClickCloseButton')
        }
    }
}
</script>
<style scoped>
    
</style>