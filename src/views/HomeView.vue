<script setup lang="ts">
import QuizForm from '@/components/QuizForm.vue'
</script>

<template>
  <!-- container-fluid permet de s'étendre sur toute la largeur de la page -->
  <div class="container-fluid mt-3">
    <!-- Centrer le contenu sur toutes les tailles d'écran -->
    <div class="row justify-content-center">
      <!-- Adaptation de la largeur selon la taille de l'écran -->
      <div class="col-12 col-md-8 col-lg-6">
        <!-- Titre de la page centré avec un soulignement -->
        <h1 class="text-center mb-10 text-decoration-underline">Quiz</h1>
        <QuizForm />
      </div>
    </div>
  </div>
</template>
<!--
col-12 : Sur les écrans très petits (mobile), l'élément occupe 100 % de la largeur.
col-md-8 : Sur les écrans moyens, qui offre une largeur raisonnable.
col-lg-6 : Sur les grands écrans, cette valeur établit un équilibre visuel avec un contenu centré, tout en laissant des marges sur les côtés.
-->
