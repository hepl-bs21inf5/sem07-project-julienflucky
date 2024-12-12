<script setup lang="ts">
import { computed, ref, watch, type PropType } from 'vue'
import { QuestionState } from '@/utils/models'

const model = defineModel<QuestionState>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  answerDetail: { type: String, default: '' },
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>,
    required: true,
  },
})

const value = ref<string | null>(null)
const answerText = computed<string>(
  () => props.options.find((option) => option.value === props.answer)?.text ?? props.answer,
)

const shuffledOptions = computed(() => {
  return props.options.slice().sort(() => Math.random() - 0.5)
})

//watch permet d'exécuter une fonction à chaque fois que value change//
//Si la valeur devient null, l'état devient Empty. Sinon, l'état devient Fill.//
watch(
  value,
  (newValue) => {
    if (newValue === null) {
      model.value = QuestionState.Empty
    } else {
      model.value = QuestionState.Fill
    }
  },
  { immediate: true },
)

watch(model, (newModel) => {
  if (newModel === QuestionState.Submit) {
    model.value = value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong
  } else if (newModel === QuestionState.Empty) {
    value.value = null
  }
})
</script>

<template>
  {{ props.text }}
  <div v-for="option in shuffledOptions" :key="option.value" class="form-check">
    <input
      :id="`${props.id}-${option.value}`"
      v-model="value"
      class="form-check-input"
      type="radio"
      :name="props.id"
      :value="option.value"
      :disabled="
        model === QuestionState.Submit ||
        model === QuestionState.Correct ||
        model === QuestionState.Wrong
      "
    />
    <!-- Les deux barres || veulent dire or -->
    <label class="form-check-label" :for="`${props.id}-${option.value}`">
      {{ option.text }}
    </label>
  </div>
  <div v-if="modelValue === QuestionState.Correct || modelValue === QuestionState.Wrong">
    <p v-if="modelValue === QuestionState.Correct" class="text-success">Juste !</p>
    <p v-else class="text-danger">Faux ! La réponse était : {{ answerText }}</p>
    <p class="blockquote-footer">{{ props.answerDetail }}</p>
  </div>
</template>

<style scoped>
.text-danger {
  color: rgb(255, 0, 217) !important;
}
</style>

<!-- Dans la partie <script>, on utilise les fonctions defineModel et defineProps pour définir le modèle (v-model)
et les propriétés (text, name, options) du composant.
Dans la partie <template> :
On affiche le texte de la question : {{ props.text }}.
On affiche les options de réponse en utilisant une boucle v-for sur props.options : le <div> sera répété pour chaque option.
La différence entre les attributs qui commencent par : et ceux qui ne commencent pas par :
est que les premiers sont des expressions JavaScript (interprétées) et les seconds sont des chaînes de caractères (non interprétées). -->
