<script setup lang="ts">
import QuestionRadio from '@/components/QuestionRadio.vue'
import { ref, computed } from 'vue'
import { QuestionState } from '@/utils/models'

interface Answer {
  value: string
  text: string
}

interface Question {
  question: string
  correct_answer: string
  incorrect_answers: string[]
}

const questions = ref<(Question & { shuffledAnswers: Answer[] })[]>([])

const questionStates = ref<QuestionState[]>([])
const score = computed<number>(
  () => questionStates.value.filter((state) => state === QuestionState.Correct).length,
)
const max_score = computed<number>(() => questions.value.length)
const filled = computed<boolean>(() =>
  questionStates.value.every((state) => state === QuestionState.Fill),
)
const submitted = computed<boolean>(() =>
  questionStates.value.every(
    (state) => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
)

function reset(event: Event): void {
  event.preventDefault()
  questionStates.value = []

  fetchNewQuestions()
}

function submit(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map((state, index) => {
    return questionStates.value[index] === QuestionState.Fill ? QuestionState.Submit : state
  })
}

function fetchNewQuestions(): void {
  fetch('https://opentdb.com/api.php?amount=10&type=multiple')
    .then((response) => response.json())
    .then((data) => {
      questions.value = data.results.map((question: Question) => {
        const allAnswers: Answer[] = [
          { value: question.correct_answer, text: question.correct_answer },
          ...question.incorrect_answers.map((answer) => ({
            value: answer,
            text: answer,
          })),
        ]
        const shuffledAnswers = shuffleArray(allAnswers)
        return { ...question, shuffledAnswers }
      })

      questionStates.value = new Array(questions.value.length).fill(QuestionState.Empty)
    })
}

function shuffleArray<T>(array: T[]): T[] {
  return array.sort(() => Math.random() - 0.5)
}

fetchNewQuestions()
</script>

<template>
  <form @submit="submit">
    <div v-for="(question, index) in questions" :key="index">
      <QuestionRadio
        :id="index.toString()"
        v-model="questionStates[index]"
        :text="question.question"
        :answer="question.correct_answer"
        :options="question.shuffledAnswers"
      />
    </div>
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <button class="btn btn-secondary" @click="reset">Réinitialiser</button>
    <div v-if="submitted">Score: {{ score }} / {{ max_score }}</div>
    <div>Debug états : {{ questionStates }}</div>
  </form>
</template>
