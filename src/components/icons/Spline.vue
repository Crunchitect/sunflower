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
        const app = new Application(canvas.value);
        await app.load(state.spline.scene)
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