<script setup lang="ts">
//Pour importer les éléments d'autres dossier ou fichier//
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import { computed, ref } from 'vue'

const cheval = ref<string | null>(null)
const chat = ref<string | null>(null)
const capitale = ref<string | null>(null)
const filled = computed<boolean>(
  () => cheval.value !== null && chat.value !== null && capitale.value !== null,
)
const reponse = ref<string | null>(null)

//Ajout du bouton reset//
function reset() {
  cheval.value = null
  chat.value = null
  capitale.value = null
  reponse.value = null
}

function submit(event: Event): void {
  //Calcul des points//
  let score = 0
  const score_parfait = 4
  let phrase: string = ''
  if (cheval.value == 'blanc') {
    score += 1
  }
  if (chat.value == 'quatre') {
    score += 1
  }
  if (capitale.value == 'bern') {
    score += 1
  }
  if (
    reponse.value == '4' ||
    reponse.value == 'quatre' ||
    reponse.value == 'quatre' ||
    reponse.value == 'quattre' ||
    reponse.value == 'Quattre'
  ) {
    score += 1
    //les deux barre || font comme un 'or' pour avoir plusieurs conditions//
  }
  if (score == score_parfait) {
    phrase = 'Parfait ! Bravo !'
  } else if (score == 0) {
    phrase = 'Dommage, tu feras mieux la prochaine fois !'
  } else if (score == 1) {
    phrase = 'Tu peux mieux faire !'
  } else if (score == 2) {
    phrase = 'Bien !'
  } else if (score == 3) {
    phrase = 'Super !'
  }
  event.preventDefault()
  if (filled.value) {
    //Message d'alerte de fin selon le score//
    alert(`Vous avez choisi la couleur ${cheval.value} !
Vous avez choisi le nombre ${chat.value} !
Vous avez choisi la capitale ${capitale.value} !
Vous avez choisi le nombre ${reponse.value} !
et votre score est de ${score}/${score_parfait} ${phrase}
`)
  }
}
</script>

<template>
  <form @submit="submit">
    <QuestionRadio
      id="cheval"
      v-model="cheval"
      text="De quelle couleur est le cheval blanc de Napoléon ?"
      :options="[
        { value: 'blanc', text: 'Blanc' },
        { value: 'brun', text: 'Brun' },
        { value: 'noir', text: 'Noir' },
        { value: 'gris', text: 'Gris' },
      ]"
    />
    <!--
v-model : la valeur de la réponse.
id : un identifiant unique pour le groupe de boutons radio.
text : le texte de la question.
options : un tableau d'objets pour les options de réponse.
-->
    <QuestionRadio
      id="chat"
      v-model="chat"
      text="Combien de pattes a un chat ?"
      :options="[
        { value: 'quatre', text: 'Quatre' },
        { value: 'trois', text: 'Trois' },
        { value: 'cinq', text: 'Cinq' },
        { value: 'deux', text: 'deux' },
      ]"
    />
    <QuestionRadio
      id="capitale"
      v-model="capitale"
      text="Quelle est la capitale de la Suisse ?"
      :options="[
        { value: 'genève', text: 'Genève' },
        { value: 'bern', text: 'Bern' },
        { value: 'zürich', text: 'Zürich' },
        { value: 'lausanne', text: 'Lausanne' },
      ]"
    />
    <QuestionText
      id="chien"
      v-model="reponse"
      text="Combien de pattes a un chien ?"
      placeholder="Veuillez saisir un nombre"
    />
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
  </form>
  <!-- bouton reset en dehors de form pour qu'il ne soit pas lié aux questions-->
  <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
</template>
