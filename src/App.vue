<script lang="ts" setup>
// All imports are automatic but if you want to import anything,
// remember to import from 'vue-termui':
// import { ref } from 'vue-termui'

const n = ref(0)
const id = ref(0)
const IsPerfectSquare = ref(false)
const IsRepeated = ref(false)
const values = ref<number[]>([0,0,0, 0,0,0, 0,0,0])

onKeyData(['+', 'ArrowRight', 'ArrowUp'], () => {
  values.value[id.value]++
})

onKeyData(['-', 'ArrowLeft', 'ArrowDown'], () => {
  if (values.value[id.value] <= 0){
    return;
  }

  values.value[id.value]--
})

onKeyData('q', () => {
  process.exit(0)
})

onKeyData('c', () => {
  console.clear()
  values.value = [0,0,0, 0,0,0, 0,0,0]
})

onKeyData('Tab', () => {
 id.value = (id.value + 1) % 9
})

const verifyPerfectSquare = () => {
  const firstRow = values.value[0] + values.value[1] + values.value[2]
  const secondRow = values.value[3] + values.value[4] + values.value[5]
  const thirdRow = values.value[6] + values.value[7] + values.value[8]

  const firstColumn = values.value[0] + values.value[3] + values.value[6]
  const secondColumn = values.value[1] + values.value[4] + values.value[7]
  const thirdColumn = values.value[2] + values.value[5] + values.value[8]

  //return !IsRepeated 
  return firstRow === secondRow 
        && secondRow === thirdRow 
        && thirdRow === firstColumn 
        && firstColumn === secondColumn 
        && secondColumn === thirdColumn
}


useInterval(() => {
  IsRepeated.value = values.value.some((value, index) => values.value.indexOf(value) !== index)
  IsPerfectSquare.value = verifyPerfectSquare();
}, 600)

</script>

<template>
  <Box
    :padding="2"
    :margin="2"
    width="100%"
    :maxWidth="50"
    flexDirection="column"
    borderColor="yellowBright"
    borderStyle="round"
  >
    <Box flexDirection="column">
      <Box>
        <Text id=0 :color="id === 0 ? 'yellow' : 'yellowBright'" :underline="id === 0" bold>{{ values[0] }}</Text>
        <Text id=1 :color="id === 1 ? 'yellow' : 'yellowBright'" :underline="id === 1" bold>{{ values[1] }}</Text>
        <Text id=2 :color="id === 2 ? 'yellow' : 'yellowBright'" :underline="id === 2" bold>{{ values[2] }}</Text>
      </Box>
      <Text>
        <Text id=3 :color="id === 3 ? 'yellow' : 'yellowBright'" :underline="id === 3" bold>{{ values[3] }}</Text>
        <Text id=4 :color="id === 4 ? 'yellow' : 'yellowBright'" :underline="id === 4" bold>{{ values[4] }}</Text>
        <Text id=5 :color="id === 5 ? 'yellow' : 'yellowBright'" :underline="id === 5" bold>{{ values[5] }}</Text>
      </Text>
      <Text>
        <Text id=6 :color="id === 6 ? 'yellow' : 'yellowBright'" :underline="id === 6" bold>{{ values[6] }}</Text>
        <Text id=7 :color="id === 7 ? 'yellow' : 'yellowBright'" :underline="id === 7" bold>{{ values[7] }}</Text>
        <Text id=8 :color="id === 8 ? 'yellow' : 'yellowBright'" :underline="id === 8" bold>{{ values[8] }}</Text>
      </Text>
    </Box>

    <Box :marginY="1">
      <Text :color="IsPerfectSquare ? 'yellow' : 'yellowBright'">{{ IsPerfectSquare ? 'Is a Perfect square 😮' : ' Is not a Perfect square 😥' }}</Text>
    </Box>
  </Box>

  <Text>
    <Text color="red" bold> -</Text>/<Text bold color="green">+</Text> to change it
  </Text>
  <Text>
    Press <Text color="yellow" bold>q</Text> to exit
  </Text>
  <Text>
    Press <Text color="yellow" bold>Tab</Text> to switch between numbers
  </Text>
  <Text>
    Press <Text color="yellow" bold>c</Text> to clear the screen
  </Text>
</template>
