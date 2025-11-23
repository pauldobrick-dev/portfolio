<!-- ./components/MainTop.vue -->
<template>
    <div class="outline-MainTop">
        <div class="text-section">
            <h1>ICH</h1>
            <span id="sub1">baue</span>
            <span id="sub2" :class="{ openBlock: isActive }">&lt;Web-Apps&gt;*</span>
            <span id="sub2sub" :class="{ moveDown: isActive }">*die funktionieren</span>
        </div>
        <div class="img-section">
            <div class="img-info-back" :class="{ openInfos: isActiveInfo }"></div>
            <img :class="{ openImg: isActiveInfo }" @mouseover="toggleInfos" src="../assets/Portfoliomain.jpg" width="450px"/>
        </div>
    </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'

const isActive = ref(false);
const isActiveInfo = ref(false);

function toggleInfos() {
    isActiveInfo.value = !isActiveInfo.value
}

onMounted(() => {
  setTimeout(() => {
    console.log("10 Sekunden sind vorbei!");
    isActive.value = true
  }, 5000);
});
</script>

<style scoped lang="scss">
@import '../assets/style.scss';

.outline-MainTop {
    display: grid;

    grid-template-rows: 0.1fr 1fr 0.1fr;
    grid-template-columns: 1fr 1fr 1fr;

    width: 100%;
    height: 100%;

    background: linear-gradient(135deg, $main-red 0%, #7f1d1d 50%, $dark-bg 100%);
}

.text-section {
    display: flex;
    justify-content: center;
    color: white;
    grid-row: 2;
    grid-column: 1;
    position: relative; 
    
    h1 {
        font-family: Almendra;
        font-weight: 700;
        font-size: 80px;
        z-index: 2;

        transform: translateX(-50px);
    }
    
    #sub1 {
        position: absolute; 
        top: 90px;        
        left: calc(50% - 50px + 50px); 
        z-index: 1;
        font-family: Lugrasimo;
        color: $accent-gold;
        font-size: 50px;
    }
    
    #sub2 {
        display: flex;

        align-items: center;
        justify-content: center;

        position: absolute; 
        top: 170px;         
        left: calc(50% - 200px + 80px); 
        z-index: 1;
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        font-style: italic;
        color: $img-blue;
        font-size: 40px;
        letter-spacing: 5px;

        background-color: white;
        
        width: 400px;
        height: 100px;

        //height: 520px;

        border-radius: 10px;

        will-change: height;
    }

    #sub2sub {
    position: absolute;
    top: 280px;  
    left: calc(50% - 200px + 140px);  
    z-index: 1;
    font-family: serif;
    font-style: italic;
    color: $text-muted;
    font-weight: 200;
    font-size: 20px;
    will-change: top;
    transition: top 1s cubic-bezier(0.4, 0, 0.2, 1);
}
}

.img-section {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding-right: 100px;
    grid-row: 2;
    grid-column: 2 / 4;
    width: 100%;
    height: 100%;
    position: relative;
    
    .img-info-back {
        position: absolute;
        width: 300px; // Anpassen
        height: 500px; 
        background-color: white;
        border-radius: 30px;
        left: 72%;
        transform: translateX(-50%) translateX(-30px);  
        z-index: 1;
        will-change: width, height; // height hinzufügen
        transition: all .5s cubic-bezier(0.4, 0, 0.2, 1);
    }
    
    img {
        width: 450px;
        border-radius: 30px;
        z-index: 2;
        position: relative;

        will-change: width, height; // height hinzufügen
        transition: all .5s cubic-bezier(0.4, 0, 0.2, 1);
    }
}

// --- VUE.JS ADDS --- //
.openBlock {
    height: 520px !important;
    transition: height 1s cubic-bezier(0.4, 0, 0.2, 1);
}

.moveDown {
    top: 700px !important;  // 170px + 520px + 10px (Anpassen nach Bedarf)
    transition: top 1s cubic-bezier(0.4, 0, 0.2, 1);
}

.openInfos {
    left: 65%!important;
    width: 600px !important;
    height: 700px!important;
    transition: all .5s cubic-bezier(0.4, 0, 0.2, 1);
}

.openImg {
    width: 300px!important;

    box-shadow: 0px 0px 20px black;
}

</style>