<template>
    <div class=" border flex rounded overflow-hidden mt-4 shadow-sm card" v-bind:class="{ 'disabled' : isActive }" v-on:click="toggleActive">
        <div class="card_image p-4">
            <div class="lights_out font-black text-sm flex justify-center border">
                <div class="cross">
                    <template v-if="isActive">X</template>
                </div>
            </div>
        </div>
        <div class="card_copy p-4 flex align-center items-center">
            <div class="flex align-center items-center">
                <h2 class="text-lg font-black">{{question}}</h2>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        img:String,
        title:String,
        desc:String,
        question:String
    },
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

<style scoped>
.card {
    transition:250ms ease;
}
.disabled {
    opacity:.5;
    background:#ededed;
}
.card_image {
    z-index:-1;
    position:relative;
    width:20%;
    overflow:hidden;
}
.lights_out {
    padding-top:100%;
}
.cross {
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
}
.card_copy {
    width:80%;
}
</style>