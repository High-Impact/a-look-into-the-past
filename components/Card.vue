<template>
    <NuxtLink :to="link" class="bg-gray-100 flex rounded overflow-hidden mt-4 shadow-sm">
        <div class="">
            <img :src="img" />
        </div>
        <div class=" p-4">
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