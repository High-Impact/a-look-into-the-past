<template>
    <a :href="link" target="blank" class=" border flex rounded overflow-hidden mt-4 shadow-sm card">
        <div class="card_image" >
            <img class="object-cover h-full w-full" :src="img" />
        </div>
        <div class="card_copy p-4">
            <div class="">
                <h2 class="text-lg font-bold">{{header}}</h2>
                <span class="text-gray-500 italic">{{dateFormater(date)}}</span>
                <p>{{desc}}</p>
            </div>
        </div>
    </a>
</template>

<script>
export default {
    props: {
        img:String,
        link:String,
        header:String,
        desc:String,
        type:String,
        weight:Number,
        date:String
    },
    methods: {
        dateFormater: function(date) {
            let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
            let year = date.slice(0,4);
            let month = months[date.slice(5,6) - 1];
            let day = date.slice(6,8);
            return `${month} ${day}, ${year}`;
        }
    }
}
</script>

<style scoped>
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