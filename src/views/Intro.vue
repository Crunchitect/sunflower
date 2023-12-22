<script setup>
    import anime from "../lib/anime";
    import { ref, onMounted } from 'vue';
    import Handwriting from '../components/icons/Handwriting.vue';
    import Spline from "../components/icons/Spline.vue";

    const sleep = ms => new Promise(r => setTimeout(r, ms));
    const lin_grad = `linear-gradient(white 0.1%, #f7ff00 10%, #ff9900 60%)`

    const start = (async () => {
        document.querySelector('.full').remove();

        let tl = anime.timeline({
          duration: 4500,
        });

        tl.add({
            targets: '.intro svg path',
            strokeDashoffset: [anime.setDashoffset, 0],
            easing: 'easeInOutSine',
            duration: 3500,
            delay: 2500,
        }).add({
          targets: ".intro",
          width: 0,
          duration: 750,
          easing: 'cubicBezier(.14,1.07,.42,1.08)'
        }).add({
          targets: ".h2",
          translateY: -1000,
          duration: 1000
        }).add({
          targets: ".slogan",
          fontSize: "3.5rem",
          opacity: 1,
          top: "95vw",
          easing: 'easeInOutSine',
          duration: 500
        });
    });
</script>

<template>
    <div class="full">
      Loading Models....
    </div>
    <div class="intro side" >
      <Handwriting class="handwriting" color="url(#linear-grad)" />
    </div>
    <div class="intro1 side">
      <Handwriting class="handwriting h2" color="white" />
    </div>
    <Spline url="https://prod.spline.design/o3eywZC60UX0rmyq/scene.splinecode" @done="start" class="spline" />
    <p class="slogan">น้ำมันนวดธรรมชาติ</p>
</template>

<style scoped>
  .slogan {
    opacity: 0;
    color: white;
    position: absolute;
    z-index: 69420;
    margin-left: 0;
    margin-right: 0;
    width: 100vw;
    text-align: center;
  }


  .full {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: white;
    z-index: 69420;
    font-size: 7rem;
    display: flex;
    flex-flow: row wrap;
    place-content: center;
  }
  .side {
    display: grid;
    height: 100vh;
    overflow: hidden;
    place-items: center;
    position: absolute;
    width: 100%;
  }
  .intro {
    z-index: 69;
    background: white;
  }

  .intro1 {
    background-image: linear-gradient(white 0.1%, #f7ff00 10%, #ff9900 60%);
    z-index: -69;
  }

  .handwriting {
    width: 80vw;
    height: auto;
    /* transform: scale(1.8); */
    margin: 10vw;
  }

  .spline {
    position: absolute;
    top: 0;
    left: 0;
    width: 100dvw;
    height: 100dvh;
    /* margin-top: 20vh; */
  }
</style>
