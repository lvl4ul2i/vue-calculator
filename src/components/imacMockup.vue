<template>
    <div>
        <img src="../assets/imac.png" alt="">
        <div class="screen">
            <div class="screen__background">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style scoped>
    img{
        width: 990px;
    }
    .screen{
        position: absolute;
        top: 60px;
        left: 50%;
        width: 915px;
        height: 510px;
    }
    .screen__background{
        background-image: url("../assets/screeenbg.jpg");
        background-color: #000;
        background-repeat: round;
        position: relative;
        margin: 0;
        padding: 0;
        left: -50%;
        width: 100%;
        height: 100%;
    }
</style>