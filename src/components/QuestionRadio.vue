<script setup lang="ts">
import { ref, watch, type PropType } from 'vue'

const model = defineModel<boolean>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>,
    required: true,
  },
})

const value = ref<string | null>(null)

//watch permet d'exécuter une fonction à chaque fois que value change//
watch(
  value,
  (newValue) => {
    model.value = newValue === props.answer
  },
  { immediate: true },
)
</script>

<template>
  {{ props.text }}
  <div v-for="option in props.options" :key="option.value" class="form-check">
    <input
      :id="`${props.id}-${option.value}`"
      v-model="model"
      class="form-check-input"
      type="radio"
      :name="props.id"
      :value="option.value"
    />
    <label class="form-check-label" :for="`${props.id}-${option.value}`">
      {{ option.text }}
    </label>
  </div>
</template>

<!-- Dans la partie <script>, on utilise les fonctions defineModel et defineProps pour définir le modèle (v-model)
et les propriétés (text, name, options) du composant.
Dans la partie <template> :
On affiche le texte de la question : {{ props.text }}.
On affiche les options de réponse en utilisant une boucle v-for sur props.options : le <div> sera répété pour chaque option.
La différence entre les attributs qui commencent par : et ceux qui ne commencent pas par :
est que les premiers sont des expressions JavaScript (interprétées) et les seconds sont des chaînes de caractères (non interprétées). -->
