<template>
  <section>
    <span>{{ number }}</span>
    <div>
      <button v-for="i in KEYS.slice(0, 9)" :key="i" @click="onClick(i)">
        {{ i }}
      </button>
      <button @click="onDelete">del</button>
      <button @click="onClick(KEYS[9])">{{ KEYS[9] }}</button>
      <button>OK</button>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const KEYS = ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0']
  .map((value) => ({ value, sort: Math.random() }))
  .sort((a, b) => a.sort - b.sort)
  .map(({ value }) => value)

const number = ref<string | null>(null)

const onClick = (num: string) => {
  number.value = number.value == null ? num : number.value + num
}

const onDelete = () => {
  if (number.value == null) return
  number.value = number.value.slice(0, number.value.length - 1)
}
</script>

<style scoped>
section {
  max-width: 24rem;
  margin: 4rem auto;
}
span {
  height: 2.8rem;
  font-size: 1.8rem;
  text-align: center;
  display: block;
  margin-block: 1rem;
  border: 1px solid #999;
  border-radius: var(--pico-border-radius);
  white-space: nowrap;
  overflow-x: hidden;
}
div {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}
button {
  background-color: #4d535e;
  border-color: #4d535e;
}

button:hover {
  transform: scale(1.05);
}
button:active {
  transform: translateY(2.5%);
  outline: none;
}
button:focus {
  outline: none;
  box-shadow: none;
}
</style>
