<script setup lang="ts">
import { ref, watch } from 'vue'

const modelValue = defineModel<boolean>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  placeholder: { type: String, default: 'Veuillez saisir une réponse' },
})

const value = ref<string | null>(null)

watch(
  value,
  (newValue) => {
    modelValue.value = newValue === props.answer
  },
  { immediate: true },
)
</script>

<template>
  <div>
    <label :for="props.id" class="form-label">
      {{ props.text }}
    </label>
    <input
      :id="props.id"
      v-model="modelValue"
      class="form-control"
      type="text"
      :placeholder="props.placeholder"
    />
  </div>
</template>

<!--
defineModel : Crée la variable qui gère la valeur liée au v-model.
defineProps : Définit les propriétés (ou props) que ce composant attend, comme id, text, et placeholder.
<label> et <input> : Crée un label lié à un input, affichant la question et permettant à l'utilisateur de saisir une réponse.
v-model : Assure une liaison bidirectionnelle entre l'input et la variable modelValue pour capturer et
manipuler la réponse de l'utilisateur.
-->
