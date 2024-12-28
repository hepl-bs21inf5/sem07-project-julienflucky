<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <RouterLink class="navbar-brand" to="/">
        <!-- changement d'icone de la dans la barre -->
        <span style="color: red"><i class="bi bi-1-circle-fill"></i></span>
        <span style="color: red"> Quiz </span>
      </RouterLink>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbar"
        aria-controls="navbar"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div id="navbar" class="collapse navbar-collapse">
        <ul class="navbar-nav">
          <li class="nav-item">
            <RouterLink class="nav-link" to="/trivia">
              <!-- changement d'icone de la dans la barre -->
              <span style="color: blue"><i class="bi bi-2-circle-fill"></i></span>
              <span style="color: blue">Trivia</span>
            </RouterLink>
          </li>

          <li class="nav-item">
            <RouterLink class="nav-link" to="/description">
              <!-- changement d'icone de la dans la barre -->
              <span style="color: green"><i class="bi bi-3-circle-fill"></i></span>
              <span style="color: green">Descriptif du module</span>
            </RouterLink>
          </li>

          <li class="nav-item">
            <RouterLink class="nav-link" to="/about">
              <!-- changement d'icone de la dans la barre -->
              <span style="color: darkmagenta"><i class="bi bi-4-circle-fill"></i></span>
              <span style="color: darkmagenta">À propos</span>
            </RouterLink>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <RouterView />
</template>
