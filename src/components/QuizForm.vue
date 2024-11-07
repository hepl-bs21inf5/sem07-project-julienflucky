<script setup lang="ts">
import { computed, ref } from 'vue'

const cheval = ref<string | null>(null)
const chat = ref<string | null>(null)
const capitale = ref<string | null>(null)
const filled = computed<boolean>(
  () => cheval.value !== null && chat.value !== null && capitale.value !== null,
)

function submit(event: Event): void {
  event.preventDefault()
  if (filled.value) {
    alert(`Vous avez choisi la couleur ${cheval.value} !
Vous avez choisi le nombre ${chat.value} !
Vous avez choisi la capitale ${capitale.value} !
`)
  }
}
</script>

<template>
  <form @submit="submit">
    De quelle couleur est le cheval blanc de Napoléon ?
    <div class="form-check">
      <input
        id="chevalBlanc"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="Blanc"
      />
      <label class="form-check-label" for="chevalBlanc">Blanc</label>
    </div>
    <div class="form-check">
      <input
        id="chevalBrun"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="Brun"
      />
      <label class="form-check-label" for="chevalBrun">Brun</label>
    </div>
    <div class="form-check">
      <input
        id="chevalNoir"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="Noir"
      />
      <label class="form-check-label" for="chevalNoir">Noir</label>
    </div>
    <div class="form-check">
      <input
        id="chevalGris"
        v-model="cheval"
        class="form-check-input"
        type="radio"
        name="cheval"
        value="Gris"
      />
      <label class="form-check-label" for="chevalGris">Gris</label>
    </div>
  </form>

  <form @submit="submit">
    Combien de pattes a un chat ?
    <div class="form-check">
      <input
        id="chatQuatre"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="Quatre"
      />
      <label class="form-check-label" for="chatQuatre">Quatre</label>
    </div>
    <div class="form-check">
      <input
        id="chatTrois"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="Trois"
      />
      <label class="form-check-label" for="chatTrois">Trois</label>
    </div>
    <div class="form-check">
      <input
        id="chatCinq"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="Cinq"
      />
      <label class="form-check-label" for="chatCinq">Cinq</label>
    </div>
    <div class="form-check">
      <input
        id="chatDeux"
        v-model="chat"
        class="form-check-input"
        type="radio"
        name="chat"
        value="Deux"
      />
      <label class="form-check-label" for="chatDeux">Deux</label>
    </div>
  </form>

  <form @submit="submit">
    Quelle est la capitale de la Suisse ?
    <div class="form-check">
      <input
        id="capitaleGeneve"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="capitale"
        value="Genève"
      />
      <label class="form-check-label" for="capitaleGeneve">Genève</label>
    </div>
    <div class="form-check">
      <input
        id="capitaleBern"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="capitale"
        value="Bern"
      />
      <label class="form-check-label" for="capitaleBern">Bern</label>
    </div>
    <div class="form-check">
      <input
        id="capitaleZurich"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="capitale"
        value="Zürich"
      />
      <label class="form-check-label" for="capitaleZurich">Zürich</label>
    </div>
    <div class="form-check">
      <input
        id="capitaleLausanne"
        v-model="capitale"
        class="form-check-input"
        type="radio"
        name="capitale"
        value="Lausanne"
      />
      <label class="form-check-label" for="capitaleLausanne">Lausanne</label>
    </div>
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
  </form>
</template>
