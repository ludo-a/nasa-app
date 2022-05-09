<template>
    <div class="modal">
        <div class="modal__inner">
            <h2>
                <slot name="title">
                </slot>
            </h2>
            <div>
                <slot>
                </slot>
            </div>
            <button class="buttonSlider" @click="$emit('closeModal')">Close</button>
        </div>
    </div>
</template>

<style scoped>
    .modal{
        width:100%;
        height:100vh;
        background:rgba(0,0,0,0.5);
        z-index:10;
        position:fixed;
        top:0;
        left:0;
        padding-top:30px;
    }

    .modal__inner{
        max-width:80%;
        min-width:20%;
        width:50%;
        padding:1em 2em;
        height:auto;
        margin:auto;
        background:white;
        border: 3px solid #fc3e2134;
        border-radius: 50px;
    }
</style>