<template>
    <div class="overflow-hidden relative min-h-screen">
        <div class="py-4 shadow-sm">
            <div class="container mx-auto px-12 flex items-center justify-between">
                <NuxtLink to="/" class="text-4xl text-gray-700 font-black capitalize ">
                    <h1 v-if="path">{{path.split('/').pop()}}</h1>
                    <h1 v-else>Home</h1>
                </NuxtLink>
                <div class="transform rotate-180 z-10">
                    <button v-on:click="toggleActive" class="hamburger hamburger--elastic focus:outline-none p-0" v-bind:class="{ 'is-active' : isActive }" type="button">
                        <span class="hamburger-box">
                            <span class="hamburger-inner"></span>
                        </span>
                    </button>
                </div>
                <div class="nav absolute bg-white h-screen w-screen" v-bind:class="{ 'active' : isActive }">
                    <div class="cheat absolute bg-white h-screen w-screen">
                        <div class="container mx-auto px-12 pt-12">
                            <h2 class="font-black text-xl">A look into the past</h2>
                            <hr class="my-8">
                            <ul class="font-bold text-4xl leading-relaxed">
                                <li>
                                    <a href="/">Home</a>
                                </li>
                                <li>
                                    <NuxtLink to="/albums">
                                        Albums
                                    </NuxtLink>
                                </li>
                                <li>
                                    <NuxtLink to="/questions">
                                        Questions
                                    </NuxtLink>
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div v-if="path" class="container mx-auto px-12 pt-4">
            <button @click="backAPage" class="text-gray-500"><fa icon="arrow-left"  /> Back</button>
        </div>
        <div class="container mx-auto px-12 pt-8 lower">
            <div class="pb-12">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isActive:false,
            path:this.$route.path.replace('/', '')
        }
    },
    methods: {
        toggleActive: function() {
            this.isActive = !this.isActive
        },
        backAPage: function() {
            window.history.go(-1);
        }
    }
}
</script>

<style>
    .nav {
        top:0;
        left:0;
        opacity:0;
        transition:375ms steps(60);
        visibility:hidden;
        z-index:9;
    }
    .nav.active {
        visibility:visible;
        opacity:.95;
    }

    .nav .cheat{
        left: 100%;
        top:0;
        transition:375ms steps(60);
    }
    .nav.active .cheat{
        left:0;
    }
    .hamburger-box span,
    .hamburger-box :before,
    .hamburger-box :after {
        background:#374151;    
    }

    .lower {
        z-index:-1;
    }
</style>