<template>
    <header class="flex items-center bg-White sticky top-0 h-[72px] lg:h-28 w-full lg:border-b border-Grayish-blue z-10">
        <button @click="clickMenuButton" class="lg:hidden flex items-center p-4 ml-2">
            <img src="../images/icon-menu.svg" alt="">
        </button>
        <div class="flex pl-0 w-full">
            <a href="" class="flex">
                <img src="../images/logo.svg" class="object-contain mt-[-0.18rem]" alt="">
            </a>
            <nav class="hidden lg:flex ml-14 gap-8 h-28">
                <div>
                    <a href="">Collections</a>
                </div>
                <div>
                    <a href="">Men</a>
                </div>
                <div>
                    <a href="">Women</a>
                </div>
                <div>
                    <a href="">About</a>
                </div>
                <div>
                    <a href="">Contact</a>
                </div>
            </nav>
            <div class="flex-auto flex place-content-end">
                <button @click="clickCartButton" class="cartButton">
                    <svg width="22" height="20" xmlns="http://www.w3.org/2000/svg"><path d="M20.925 3.641H3.863L3.61.816A.896.896 0 0 0 2.717 0H.897a.896.896 0 1 0 0 1.792h1l1.031 11.483c.073.828.52 1.726 1.291 2.336C2.83 17.385 4.099 20 6.359 20c1.875 0 3.197-1.87 2.554-3.642h4.905c-.642 1.77.677 3.642 2.555 3.642a2.72 2.72 0 0 0 2.717-2.717 2.72 2.72 0 0 0-2.717-2.717H6.365c-.681 0-1.274-.41-1.53-1.009l14.321-.842a.896.896 0 0 0 .817-.677l1.821-7.283a.897.897 0 0 0-.87-1.114ZM6.358 18.208a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm10.015 0a.926.926 0 0 1 0-1.85.926.926 0 0 1 0 1.85Zm2.021-7.243-13.8.81-.57-6.341h15.753l-1.383 5.53Z" fill="#69707D" fill-rule="nonzero"/></svg>
                    <span v-if="cartCount" class="absolute top-2 lg:top-10 right-1 bg-Orange rounded-2xl px-2 text-[0.6rem] text-White">{{ cartCount }}</span>
                </button>
                <button class="avatarButton">
                    <img src="../images/image-avatar.png" alt="">
                </button>
            </div>
        </div>
    </header>
</template>
<script>
export default {
    props: ['cartCount'],
    methods: {
        clickMenuButton(){
            this.$emit('onClickMenuButton')
        },
        clickCartButton(){
            this.$emit('onClickCartButton')
        }
    }
}
</script>
<style>
nav > div {
    @apply
        transition-[border]
        flex
        items-center
        text-Dark-grayish-blue
        border-b-4
        border-Orange
        border-opacity-0
        hover:border-opacity-100
}

nav > div > a {
    @apply
        transition-colors
        -mb-1
}

nav > div > a:hover {
    @apply
        text-Very-dark-blue
}

.cartButton {
    @apply
        p-[0.625rem]
        lg:mr-6 
        relative
}

.cartButton:hover > svg > path {
    @apply
        transition-colors
        fill-Very-dark-blue
}

.avatarButton {
    @apply
        p-[0.625rem] mr-3 lg:mr-0
}

.avatarButton > img {
    @apply
        transition-[outline]
        w-6 
        lg:w-12 
        rounded-full 
        outline 
        outline-2
        outline-[hsla(0,0%,0%,0)]
        hover:outline-Orange
}
</style>