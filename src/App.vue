<script lang="ts" setup>

const id = ref(0)
const IsPerfectSquare = ref(false)
const IsRepeated = ref(false)
const values = ref<number[]>([0,0,0, 0,0,0, 0,0,0])

onMounted(() => {
  console.clear()
})

onKeyData(['+', 'ArrowRight', 'ArrowUp'], () => {
  if(values.value[id.value] >= 99){
    return;
  }
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
  id.value = 0
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

  return !IsRepeated.value
        && firstRow === secondRow 
        && secondRow === thirdRow 
        && thirdRow === firstColumn 
        && firstColumn === secondColumn 
        && secondColumn === thirdColumn
}


useInterval(() => {
  IsRepeated.value = values.value.some((value, index) => values.value.indexOf(value) !== index)
  IsPerfectSquare.value = verifyPerfectSquare();
}, 500)

</script>

<template>
  <Box
    flexDirection="column"
   :borderColor="IsPerfectSquare ? 'yellow' : 'gray'"
    borderStyle="arrow"
  >
    <Box flexDirection="column">
      <Box alignSelf="center">
        <Box 
          alignItems="center"
          justifyContent="center"
          :borderColor="IsPerfectSquare ? 'yellow' : id === 0 ? 'blue' : 'gray'"
          borderStyle="classic"
          width="30%"
        >
          <Text id=0 :color="IsPerfectSquare ? 'yellow' : id === 0 ? 'blue' : 'black'" :underline="id === 0" bold>{{ values[0] }}</Text>
        </Box>

        <Box 
          alignItems="center"
          justifyContent="center"
          :borderColor="IsPerfectSquare ? 'yellow' : id === 1 ? 'blue' : 'gray'"
          borderStyle="classic"
          width="30%"
        >
          <Text id=1 :color="IsPerfectSquare ? 'yellow' : id === 1 ? 'blue' : 'black'" :underline="id === 1" bold>{{ values[1] }}</Text>
        </Box>

        <Box 
          alignItems="center"
          justifyContent="center"
          :borderColor="IsPerfectSquare ? 'yellow' : id === 2 ? 'blue' : 'gray'"
          borderStyle="classic"
          width="30%"
        >
          <Text id=2 :color="IsPerfectSquare ? 'yellow' : id === 2 ? 'blue' : 'black'" :underline="id === 2" bold>{{ values[2] }}</Text>
        </Box>
      </Box>

      <Box alignSelf="center">
        <Box 
          alignItems="center"
          justifyContent="center"
          :borderColor="IsPerfectSquare ? 'yellow' : id === 3 ? 'blue' : 'gray'"
          borderStyle="classic"
          width="30%"
        >
          <Text id=3 :color="IsPerfectSquare ? 'yellow' : id === 3 ? 'blue' : 'black'" :underline="id === 3" bold>{{ values[3] }}</Text>
        </Box>

        <Box 
          alignItems="center"
          justifyContent="center"
          :borderColor="IsPerfectSquare ? 'yellow' : id === 4 ? 'blue' : 'gray'"
          borderStyle="classic"
          width="30%"
        >
          <Text id=4 :color="IsPerfectSquare ? 'yellow' : id === 4 ? 'blue' : 'black'" :underline="id === 4" bold>{{ values[4] }}</Text>
        </Box>

        <Box 
          alignItems="center"
          justifyContent="center"
          :borderColor="IsPerfectSquare ? 'yellow' : id === 5 ? 'blue' : 'gray'"
          borderStyle="classic"
          width="30%"
        >
          <Text id=5 :color="IsPerfectSquare ? 'yellow' : id === 5 ? 'blue' : 'black'" :underline="id === 5" bold>{{ values[5] }}</Text>
        </Box>
      </Box>

      <Box alignSelf="center">
        <Box 
          alignItems="center"
          justifyContent="center"
          :borderColor="IsPerfectSquare ? 'yellow' : id === 6 ? 'blue' : 'gray'"
          borderStyle="classic"
          width="30%"
        >
          <Text id=6 :color="IsPerfectSquare ? 'yellow' : id === 6 ? 'blue' : 'black'" :underline="id === 6" bold>{{ values[6] }}</Text>
        </Box>

        <Box 
          alignItems="center"
          justifyContent="center"
          :borderColor="IsPerfectSquare ? 'yellow' : id === 7 ? 'blue' : 'gray'"
          borderStyle="classic"
          width="30%"
        >
          <Text id=7 :color="IsPerfectSquare ? 'yellow' : id === 7 ? 'blue' : 'black'" :underline="id === 7" bold>{{ values[7] }}</Text>
        </Box>

        <Box 
          alignItems="center"
          justifyContent="center"
          :borderColor="IsPerfectSquare ? 'yellow' : id === 8 ? 'blue' : 'gray'"
          borderStyle="classic"
          width="30%"
        >
          <Text id=8 :color="IsPerfectSquare ? 'yellow' : id === 8 ? 'blue' : 'black'" :underline="id === 8" bold>{{ values[8] }}</Text>
        </Box>
      </Box>

      <Box 
        :marginY="1"
        alignSelf="center"
      >
        <Text :color="IsPerfectSquare ? 'yellow' : 'magentaBright'">{{ IsPerfectSquare ? '✧ Is a magic square ˃ᴗ˂ ✧ ' : ' Is not a magic square ಥ_ಥ' }}</Text>
      </Box>
    </Box>
  </Box>

  <Text>
    <Text color="magentaBright" bold> -</Text>/<Text bold color="blue">+</Text> to change it
  </Text>

  <Text>
    Press <Text color="blue" bold>q</Text> to exit
  </Text>

  <Text>
    Press <Text color="blue" bold>Tab</Text> to switch between numbers
  </Text>

  <Text>
    Press <Text color="blue" bold>c</Text> to clear the screen
  </Text>
</template>
