<script setup lang="ts">
import QRCode from 'qrcode';

const canvas: Ref<null | HTMLCanvasElement> = ref(null);
const width = 200;

const saveEnabled = ref(false);

async function generateQR(link: string) {
    try {
        await QRCode.toCanvas(canvas.value, link, { width });
        saveEnabled.value = true;
    } catch(err) {
        console.error(err);
    }
}

async function saveQRCode() {
    try {
        if (canvas.value) {
            const dataUrl = canvas.value.toDataURL('image/png');
            const link = document.createElement('a');
            link.href = dataUrl;
            link.download = 'qrcode.png';
            link.click();
        }
    } catch (err) {
        console.error(err);
    }
}

function cleanCanvas() {
    if(canvas.value) {
        const context = canvas.value.getContext('2d');
        if(!context) return;
        context.clearRect(0, 0, canvas.value.width, canvas.value.height);
    }
}

defineExpose({
    generateQR,
    cleanCanvas,
});

</script>

<template>
  <div class="flex flex-col gap-3 w-fit mx-auto">
    <div class="mx-auto bg-white rounded-lg p-2 flex">
      <canvas :width="`${width}px`" :height="`${width}px`" class="m-auto" ref="canvas" />
    </div>

    <UButton
        @click="saveQRCode"
        :disabled="!saveEnabled"
        variant="outline"
        block
        size="lg"
        icon="i-heroicons-arrow-down-tray-20-solid"
    >
        Télécharger
    </UButton>
  </div>

</template>

<style scoped>
canvas {
    width: 200px !important;
    height: 200px !important;
}
</style>