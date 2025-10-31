<script setup lang="ts">
// Utilisation de new URL(..., import.meta.url) pour référencer les assets (vite-compatible)
const dosDeCartes = new URL('../asset/dosDeCartes.jpg', import.meta.url).href;
const ghost = new URL('../asset/ghost.jpg', import.meta.url).href;
const ghoul = new URL('../asset/ghoul.jpg', import.meta.url).href;
const pumpkin = new URL('../asset/pumpkin.jpg', import.meta.url).href;
const witch = new URL('../asset/witch.jpg', import.meta.url).href;

// Images de base (8)
const baseImages: string[] = [
  dosDeCartes, dosDeCartes, dosDeCartes, dosDeCartes,
  ghost, ghoul, witch, pumpkin
];

// Liste des images possibles pour l'aléatoire (pool)
const lot: string[] = [ghost, ghoul, witch, pumpkin];

// On choisit UNE image aléatoire, puis on crée un tableau contenant cette même image 2 fois
const aleatoireIndex = Math.floor(Math.random() * lot.length);
const aleatoireImage: string = (lot[aleatoireIndex] ?? lot[0])!;
const aleatoire: string[] = [aleatoireImage, aleatoireImage];

// Construire le tableau final SANS utiliser les opérateurs de fusion (...)
const images: string[] = [];
for (const img of baseImages) {
  images.push(img);
}
for (const img of aleatoire) {
  images.push(img);
}
</script>

<template>
  <div class="carte">
    <img
      v-for="(image, index) in images"
      :key="index"
      class="card"
      :src="image"
      :alt="'Image ' + (index + 1)"
    />
  </div>
</template>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.carte {
  display: grid;
  grid-template-columns: repeat(2, 150px);
  grid-auto-rows: 150px; /* toutes les lignes ont même taille */
  gap: 15px;
  width: 100vw;
  height: 100vh;
  place-content: center;
}

.card {
  border: 2px solid rgb(233, 171, 88);
  border-radius: 5px;
  width: 150px;
  height: 150px;
  display: block;
  object-fit: cover;
  object-position: center;
}
</style>
