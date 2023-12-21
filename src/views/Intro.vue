<script setup>
    import anime from "../lib/anime";
    import { ref, onMounted } from 'vue';
    import Handwriting from '../components/icons/Handwriting.vue';

    const sleep = ms => new Promise(r => setTimeout(r, ms));
    const lin_grad = `linear-gradient(white 0.1%, #f7ff00 10%, #ff9900 60%)`

    onMounted(async () => {
        anime({
            targets: '.intro svg path',
            strokeDashoffset: [anime.setDashoffset, 0],
            easing: 'easeInOutSine',
            duration: 3500,
            delay: anime.stagger(150),
        });
        await sleep(3500);
        document.querySelector('.intro svg path')
            .attributes
            .stroke
            .value = "white";
        document.querySelector('.intro').style.background = lin_grad;
        document.querySelector('.intro').style.backgroundPosition = '1000%';
    });
</script>

<template>
    <div class="intro">
    <Handwriting class="handwriting" />
    </div>
</template>

<style scoped>
  .intro {
    width: 100dvw;
    height: 100dvh;
    display: flex;
    flex-flow: row wrap;
    place-content: center;
  }

  .handwriting {
    transform: scale(1.8);
  }
</style>
