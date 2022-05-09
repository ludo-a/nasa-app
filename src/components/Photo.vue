<template>
    <figure>
        <iframe v-if="media_type == 'video'" id="ytplayer" type="text/html" width="640" height="360" :src="url"
        frameborder="0"/>
        <img v-else class="pictureCss" :src="url" :alt="title + 'prise par' +copyright" />
        <figcaption>
            <h2>{{ title }} || {{ formattedDate }}</h2>
            <p>{{ explanation }}</p>
            <a href="#haut"><button class="buttonSlider"><i class="fa-solid fa-arrow-turn-up fa-2xl"></i></button></a>
        </figcaption>
    </figure>
</template>

<script>
    export default {
        props:{
            url: {
                type:String,
                required:true,
                default:'https://image-par-defaut.png',
            },

            title: {
                type:String,
                required:true,
            },

            media_type:{
                type:String,
                required:true,
                default:"image"
            },

            date: {
                type:Date,
                required:true,
                default:Date.now(),
            },

            explanation: {
                type:String,
                required:true,
            },

            copyright:{
                type:String,
                required:false,
                default:'Ludovic',
            }  
        },
        computed: {
            formattedDate() {
                let date = this.date;
                let day = Number(date.getDate()) >= 10 ? date.getDate() : '0'+date.getDate();
                return `${day}/${date.getMonth()+1}/${date.getFullYear()}`
            }
        }
    }
</script>

<style>
.pictureCss{
    max-width: 90%;
    border-radius: 5px;
}
</style>