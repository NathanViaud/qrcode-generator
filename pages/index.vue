<script setup lang="ts">
import QRCode from '~/components/QRCode.vue';

const link = ref('');

const qrcode: Ref<null | InstanceType<typeof QRCode>> = ref(null);

// Get direct download link for certain services
function transformLink() {
    if(link.value.includes('drive.google.com')) {
        link.value = link.value.replace('file/d/', 'uc?id=');
        link.value = link.value.replace('/view?usp=sharing', '&export=download');
    } else if(link.value.includes('dropbox.com')) {
        link.value = link.value.replace('www.dropbox.com', 'dl.dropboxusercontent.com');
    }
}

const qrCodeLoading = ref(false);

async function generateQR() {
    if(!qrcode.value) return;
    qrCodeLoading.value = true;

    qrcode.value.cleanCanvas();
    transformLink();

    // Wait to notify the user of changes
    await new Promise(resolve => setTimeout(resolve, 300));
    await qrcode.value.generateQR(link.value);

    qrCodeLoading.value = false;
}

</script>

<template>
    <UContainer class="max-w-4xl flex flex-col gap-5">

        <QRCode ref="qrcode" />

        <UFormGroup size="xl" label="Lien">
            <UInput
                v-model="link"
                placeholder="www.google.com"
                icon="i-heroicons-link-20-solid"
                @keydown.enter="generateQR"
            />
        </UFormGroup>

        <UButton @click="generateQR" size="xl" block :loading="qrCodeLoading">Générer le QRCode</UButton>
    </UContainer>
</template>