<template>
  <div class="tasks">
    <h1>TajpSkrypt</h1>
    <div v-for="(result, index) in results" :key="index">
      <h2>Úkol {{ index + 1 }}</h2>
      <pre>{{ result }}</pre>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue'

// Car
interface Car {
  make: string
  model: string
  year: number
}

function identity<T>(arg: T): T {
  return arg
}

export default defineComponent({
  name: 'Tasks',
  setup() {
    const results = ref<string[]>([])

    // Ruzne typy promennych
    const stringVar: string = 'Hello, TypeScript!'
    const numberVar: number = 42
    const booleanVar: boolean = !true
    const numberArray: number[] = [1, 2, 3, 4, 5]

    // Funkce multiply
    function multiply(a: number, b: number, showResult?: boolean): number {
      const result = a * b
      if (showResult) {
        console.log(`Výsledek násobení: ${result}`)
      }
      return result
    }

    // getFullName
    function getFullName(firstName: string, lastName: string): string {
      return `${firstName} ${lastName}`
    }

    // 4 Funkce greet
    function greet(name: string, greeting: string = 'Hello'): string {
      return `${greeting}, ${name}!`
    }

    function printId(id: number | string): void {
      console.log(`ID je typu ${typeof id} a má hodnotu: ${id}`)
    }

    onMounted(() => {
      // !!onMounted nacita obsah az po nacteni stranky!
      results.value.push(
        `Proměnné: ${stringVar}, ${numberVar}, ${booleanVar}, [${numberArray.join(', ')}]`
      )
      results.value.push(`Násobení: ${multiply(5, 3, true)}`)

      results.value.push(`Celé jméno: ${getFullName('John', 'Pork')}`)

      const myCar: Car = {
        make: 'Toyota',
        model: 'Corolla',
        year: 2022
      }
      results.value.push(`Auto: ${myCar.make} ${myCar.model}`)

      // 4
      results.value.push(greet('Alice'))
      results.value.push(greet('Bob', 'Hi'))

      // 5
      printId(101)
      printId('202')
      results.value.push('Výsledky úkolu 5 jsou v konzoli')

      // 6
      results.value.push(`Identity funkce s číslem: ${identity(42)}`)
      results.value.push(`Identity funkce s řetězcem: ${identity('Hello')}`)
    })

    return {
      results
    }
  }
})
</script>

<style scoped></style>
