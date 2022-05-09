<template>
    <div>
        <button class="buttonSlider" @click="slide(-1)"><i class="fa-solid fa-left-long fa-2xl"></i></button>
        <button class="buttonSlider" @click="slide(1)"><i class="fa-solid fa-right-long fa-2xl"></i></button>
        <template v-for="(slide,key) in slides" :key="key">
            <div v-if="index === key">
                <slot :slide="slide"></slot>
            </div>
        </template>
    </div>
</template>

<script>
    export default {
        props: ['slides'],
        data() {
            return {
                index:0,
            }
        },
        methods:{
           slide(operation){
               this.index = (((this.index + operation)%this.slides.length)+this.slides.length)%this.slides.length
           }
        }
    }
</script>

<style>
    .buttonSlider{
        margin-top: 20px;
        width:100px;
        height:50px;
        color:#265ebe;
        background-color: rgba(220, 216, 216, 0.796);
        border: 3px solid #fc3e2134;
        margin-left: 5px;
        margin-right: 5px;
        border-radius: 10px;
    }
</style>    