<template>
    <div>
        <div class="py-8 bg-gray-100">
            <div class="container mx-auto px-12 flex justify-between">
                <NuxtLink to="/" class="text-4xl font-black ">
                    <h1 v-if="$route.path == '/'">Home</h1>
                    <h1 v-else>{{$route.path}}</h1>
                </NuxtLink>
                <div class="transform rotate-180 z-10">
                    <button v-on:click="toggleActive" class="hamburger hamburger--arrow focus:outline-none" v-bind:class="{ 'is-active' : isActive }" type="button">
                        <span class="hamburger-box">
                            <span class="hamburger-inner"></span>
                        </span>
                    </button>
                </div>
                <div class="nav absolute bg-white h-screen w-screen" v-bind:class="{ 'active' : isActive }">
                    <div class="container mx-auto px-12 pt-12">
                        <h2 class="font-black text-xl">A look into the past</h2>
                        <hr class="my-8">
                        <ul class="font-bold text-4xl leading-relaxed">
                            <li>Home</li>
                            <li>Questions</li>
                            <li>Albums</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        <div class="container mx-auto px-12 mt-8">
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isActive:false
        }
    },
    methods: {
        toggleActive: function() {
            this.isActive = !this.isActive
        }
    }
}
</script>

<style>
    .nav {
        left: 100%;
        transition:var(--trans-norm);
    }
    .nav.active {
        transition:var(--trans-norm);
        top:0;
        left:0;
    }
</style>