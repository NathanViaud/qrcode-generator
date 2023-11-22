<script setup lang="ts">

const icon = ref('');
function changeTheme() {
    const html = document.querySelector('html');
    if (html) {
        if(html.classList.contains('dark')) html.classList.remove('dark');
        else html.classList.add('dark');

        icon.value = html.classList.contains('dark') ?  'i-heroicons-moon-20-solid' : 'i-heroicons-sun-20-solid';
    }
}

onMounted(() => {
    const html = document.querySelector('html');
    if (!html) return;
    icon.value = html.classList.contains('dark') ? 'i-heroicons-sun-20-solid' : 'i-heroicons-moon-20-solid';
})
</script>

<template>
    <nav class="flex p-5 border-b border-slate-300 dark:border-slate-700 backdrop-blur-md sticky top-0">
        <h1 class="flex-1">QRCode Generator</h1>

        <div class="flex gap-3">
            <NuxtLink to="/">Générateur</NuxtLink>
            <NuxtLink to="/help">À propos</NuxtLink>
        </div>

        <UDivider class="w-10" orientation="vertical"/>

        <UButton
            @click="changeTheme"
            square
            variant="ghost"
            color="gray"
            :icon="icon"
        />
    </nav>
</template>

<style scoped>
a {
    @apply text-lg flex m-auto;
}
</style>