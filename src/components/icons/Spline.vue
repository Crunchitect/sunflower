<script setup>
    import { ref, reactive, defineEmits, onMounted } from 'vue';
    import { Application } from '@splinetool/runtime';

    const props = defineProps({
        url: String
    });

    const emit = defineEmits(['done']);

    // template ref
    const canvas = ref(null)

    // spline state
    const state = reactive({
        spline: {
            scene: props.url,
            app: null,
            isLoaded: false,
        },
    });

    onMounted(async () =>{
        let app = new Application(canvas.value);
        await app.load(state.spline.scene).then(() => {
            let bottle = app.findObjectByName('Group');
            bottle.position.y += 40;
            document.addEventListener('scroll', () => {
                bottle.rotation.y += 0.05;
            });
            setInterval(() => bottle.rotation.y += 0.01, 75);
        });
        state.spline.app = app;
        state.spline.isLoaded = true;
        console.log('done')
        emit('done');
    })

</script>

<template>
    <section>
        <canvas ref="canvas"></canvas>
    </section>
</template>