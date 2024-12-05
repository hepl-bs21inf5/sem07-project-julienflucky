<script setup lang="ts">
//Pour importer les éléments d'autres dossier ou fichier//
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import { QuestionState } from '@/utils/models'
import { computed, ref } from 'vue'

const filled = computed<boolean>(() =>
  questionStates.value.every((state) => state === QuestionState.Fill),
)
const submitted = computed<boolean>(() =>
  questionStates.value.every(
    (state) => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
)
const questionStates = ref<QuestionState[]>([])
const score = computed<number>(
  () => questionStates.value.filter((state) => state === QuestionState.Correct).length,
)
const totalScore = computed<number>(() => questionStates.value.length)

//Ajout du bouton reset//
function reset(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Empty)
}

function submit(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Submit)
}
</script>

<template>
  <form @submit="submit">
    <!-- Question 1 -->
    <QuestionRadio
      id="cheval"
      v-model="questionStates[0]"
      text="De quelle couleur est le cheval blanc de Napoléon ?"
      :options="[
        { value: 'blanc', text: 'Blanc' },
        { value: 'brun', text: 'Brun' },
        { value: 'noir', text: 'Noir' },
        { value: 'gris', text: 'Gris' },
      ]"
      answer="blanc"
    />
    <!--
v-model : la valeur de la réponse.
id : un identifiant unique pour le groupe de boutons radio.
text : le texte de la question.
options : un tableau d'objets pour les options de réponse.
-->

    <!-- Question 2 -->
    <QuestionRadio
      id="chat"
      v-model="questionStates[1]"
      text="Combien de pattes a un chat ?"
      :options="[
        { value: 'quatre', text: 'Quatre' },
        { value: 'trois', text: 'Trois' },
        { value: 'cinq', text: 'Cinq' },
        { value: 'deux', text: 'Deux' },
      ]"
      answer="quatre"
    />

    <!-- Question 3 -->
    <QuestionRadio
      id="capitale"
      v-model="questionStates[2]"
      text="Quelle est la capitale de la Suisse ?"
      :options="[
        { value: 'genève', text: 'Genève' },
        { value: 'bern', text: 'Bern' },
        { value: 'zürich', text: 'Zürich' },
        { value: 'lausanne', text: 'Lausanne' },
      ]"
      answer="bern"
    />

    <!-- Question 4 -->
    <QuestionText
      id="chien"
      v-model="questionStates[3]"
      text="Combien de pattes a un chien ?"
      placeholder="Veuillez saisir un nombre"
      answer="4"
    />
    <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div>
    <div>Debug états : {{ questionStates }}</div>
    <button class="btn btn-primary" :class="{ disabled: !filled }" @click="submit">Terminer</button>
  </form>
  <!-- bouton reset en dehors de form pour qu'il ne soit pas lié aux questions-->
  <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
</template>
