<template>
    <div class="flex flex-col">
        <h2>À propos</h2>
        <p>Ce site permet de générer et de transformer des liens en QRCode.</p>
        <p>Le but principal de ce site est de générer des QRCode pour des liens de téléchargement direct. Il modifie
            par défaut certains liens pour les transformer en liens directs. Les services pour lesquels les liens sont modifiés sont :</p>
        <ul>
            <li>Google Drive</li>
            <li>Dropbox</li>
        </ul>
    </div>
</template>

<style scoped>
h2 {
    @apply mb-3;
}

p {
    @apply mb-1;
}

li {
    @apply list-disc ml-3;
}

</style>