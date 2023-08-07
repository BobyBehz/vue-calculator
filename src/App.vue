<template>
  <div class="container">
    <div class="calculator w-[40%] m-auto mt-[10vh] bg-black text-white">
      <div class="display border-b-2 border-orange-700 flex justify-between text-3xl py-10 px-10">
        {{ updateScreen }}
        <button @click="reset()" class="text-orange-600 ml-auto mr-0">
          Del
        </button>
      </div>
      <div class="buttons flex">
        <div class="numbers basis-3/5 flex flex-wrap">
          <div v-for="number in buttonNumbers" class="basis-1/3 aspect-square hover:bg-opacity-70 duration-300 bg-gray-800 border border-orange-700">
            <NumberButtons @put="putNumber(number)" :number="number"/>
          </div>
        </div>
        <div class="operators basis-2/5 flex flex-wrap">
          <div v-for="operator in operations" class="basis-1/2 aspect-square bg-gray-700 hover:bg-opacity-90 duration-300 border border-orange-700">
            <OperativeButtons @operate="putOperator(operator)" :operator="operator"/>
          </div>
          <button @click="putNumber(0)"
            class="basis-1/2 aspect-square bg-gray-800 hover:bg-opacity-70 duration-300 border border-orange-700">
            0
          </button>
          <button @click="operate()"
            class="basis-1/2 aspect-square bg-gray-700 hover:bg-opacity-90 duration-300 border border-orange-700">
            =
          </button>
        </div>
      </div>
    </div>


  </div>
</template>

<script setup>
import { computed, onMounted, ref } from 'vue';

import NumberButtons from '@/components/numberButtons.vue'
import OperativeButtons from '@/components/OperativeButtons.vue'

const leftSide = ref('')
const rightSide = ref('')
const operator = ref('')
const result = ref('')

const buttonNumbers = ref([])
const operations = ['+', '-', '*', '/']

const generateNumbers = onMounted(() => {
  for (let i = 1; i < 10; i++) {
    buttonNumbers.value.push(i)
  }
})

const putNumber = (number) => {
  if (!operator.value.length) {
    if (leftSide.value === '0') {
      leftSide.value = number
    } else {
      leftSide.value += `${number}`
    }
  } else {
    if (rightSide.value === '0') {
      rightSide.value = number
    } else {
      rightSide.value += `${number}`
    }
  }
}
const putOperator = (sign) => {
  if (leftSide.value.length) {
    operator.value = sign
  }
}
const reset = () => {
  leftSide.value = ''
  rightSide.value = ''
  operator.value = ''
  result.value = ''
}
const adder = () => {
  result.value = parseInt(leftSide.value) + parseInt(rightSide.value)
  result.value = `${result.value}`
}
const subtracter = () => {
  result.value = parseInt(leftSide.value) - parseInt(rightSide.value)
  result.value = `${result.value}`
}
const multiplier = () => {
  result.value = parseInt(leftSide.value) * parseInt(rightSide.value)
  result.value = `${result.value}`
}
const devider = () => {
  result.value = parseInt(leftSide.value) / parseInt(rightSide.value)
  result.value = `${result.value}`
}

const operate = () => {
  switch (operator.value) {
    case '+':
      adder()
      break
    case '-':
      subtracter()
      break
    case '*':
      multiplier()
      break
    case '/':
      devider()
      break
  }
}

const updateScreen = computed(() => {
  return `${leftSide.value} ${operator.value} ${rightSide.value} ${result.value.length ? `= ${result.value}` : ''}`
})

</script>

<style scoped></style>