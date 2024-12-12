<script setup lang="ts">
import { ref, watch } from 'vue'
import { QuestionState } from '@/utils/models'

const modelValue = defineModel<QuestionState>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answers: { type: Array as () => string[], required: true },
  answerDetail: { type: String, default: '' },
  placeholder: { type: String, default: 'Veuillez saisir une réponse' },
})

const value = ref<string | null>(null)

watch(
  value,
  (newValue) => {
    if (newValue === null) {
      modelValue.value = QuestionState.Empty
    } else {
      modelValue.value = QuestionState.Fill
    }
  },
  { immediate: true },
)

watch(modelValue, (newModel) => {
  if (newModel === QuestionState.Submit) {
    const isCorrect = props.answers.some(
      (answer) => answer.trim().toLowerCase() === (value.value || '').trim().toLowerCase(),
    )
    modelValue.value = isCorrect ? QuestionState.Correct : QuestionState.Wrong
  } else if (newModel === QuestionState.Empty) {
    value.value = null
  }
})
</script>

<template>
  <div>
    <label :for="props.id" class="form-label">
      {{ props.text }}
    </label>
    <input
      :id="props.id"
      v-model="value"
      class="form-control"
      type="text"
      :placeholder="props.placeholder"
      :disabled="
        modelValue === QuestionState.Submit ||
        modelValue === QuestionState.Correct ||
        modelValue === QuestionState.Wrong
      "
    />
  </div>
  <div v-if="modelValue === QuestionState.Correct || modelValue === QuestionState.Wrong">
    <p v-if="modelValue === QuestionState.Correct" class="text-success">Juste !</p>
    <p v-else class="text-danger">Faux ! La réponse était : {{ answers[0] }}</p>
    <p class="blockquote-footer">{{ props.answerDetail }}</p>
  </div>
</template>

<style scoped>
.text-danger {
  color: rgb(255, 0, 217) !important;
}
</style>

<!--v-if permet d'afficher une balise HTML si la condition est vraie.
v-else est lié au dernier v-if et affiche une balise HTML si la condition du v-if est fausse.
class="text-success" et class="text-danger" permettent de changer la couleur du texte avec Bootstrap.
class="blockquote-footer" a été utilisé pour afficher les détails. -->

<!--
defineModel : Crée la variable qui gère la valeur liée au v-model.
defineProps : Définit les propriétés (ou props) que ce composant attend, comme id, text, et placeholder.
<label> et <input> : Crée un label lié à un input, affichant la question et permettant à l'utilisateur de saisir une réponse.
v-model : Assure une liaison bidirectionnelle entre l'input et la variable modelValue pour capturer et
manipuler la réponse de l'utilisateur.
-->
