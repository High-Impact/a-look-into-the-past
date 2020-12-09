<template>
    <NuxtLink :to="link" class=" border flex rounded overflow-hidden mt-4 shadow-sm card">
        <div class="card_image" >
            <img class="object-cover h-full w-full" :src="img" />
        </div>
        <div class="card_copy p-4">
            <div class="">
                <h2 class="text-lg font-bold">{{title}}</h2>
                <p>{{desc}}</p>
            </div>
        </div>
    </NuxtLink>
</template>

<script>
export default {
    props: {
        img:String,
        title:String,
        desc:String,
        link:String
    }
}
</script>

<style>
.card_image {
    z-index:-1;
    position:relative;
    width:35%;
    overflow:hidden;
}
.card_copy {
    width:65%;
}
</style>