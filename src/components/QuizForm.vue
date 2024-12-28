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
      id="naruto"
      v-model="questionStates[0]"
      text="Qui est le père de Naruto ?"
      :options="[
        { value: 'minato', text: 'Minato' },
        { value: 'jiraya', text: 'Jiraya' },
        { value: 'shikamaru', text: 'Shikamaru' },
        { value: 'itachi', text: 'Itachi' },
      ]"
      answer="minato"
      answer-detail="Désolé du spoil !"
    />
    <!--
v-model : la valeur de la réponse.
id : un identifiant unique pour le groupe de boutons radio.
text : le texte de la question.
options : un tableau d'objets pour les options de réponse.
-->

    <!-- Question 2 -->
    <QuestionRadio
      id="luffy"
      v-model="questionStates[1]"
      text="Qui est le frère de Luffy ?"
      :options="[
        { value: 'ace', text: 'Ace' },
        { value: 'zoro', text: 'Zoro' },
        { value: 'usopp', text: 'Usopp' },
        { value: 'sanji', text: 'Sanji' },
      ]"
      answer="ace"
      answer-detail="Il a également un autre frère qui se nomme Sabo."
    />

    <!-- Question 3 -->
    <QuestionRadio
      id="Eren"
      v-model="questionStates[2]"
      text="Qui est le demi-frère d'Eren Jager"
      :options="[
        { value: 'reiner', text: 'Reiner' },
        { value: 'armin', text: 'Armin' },
        { value: 'sieg', text: 'Sieg' },
        { value: 'jean', text: 'Jean' },
      ]"
      answer="sieg"
      answer-detail="Ils ont le même père mais pas la même mère."
    />

    <!-- Question 4 -->
    <QuestionText
      id="izuku"
      v-model="questionStates[3]"
      text="Quel âge à Midoriya Izuku au début du manga dans l'anime My Hero Academia"
      placeholder="Veuillez saisir un nombre"
      :answers="['14', 'quatorze']"
      answer-detail="A la fin du manga il a 15 ans."
    />
    <!-- Les deux-points devant answers passe l'expression JavaScript dynamique plutôt qu'une chaîne de caractères statique.-->
    <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div>
    <button class="btn btn-primary" :class="{ disabled: !filled }" @click="submit">Terminer</button>
  </form>
  <!-- bouton reset en dehors de form pour qu'il ne soit pas lié aux questions-->
  <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
</template>
