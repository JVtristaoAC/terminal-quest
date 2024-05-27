<script lang="ts" setup>

interface SquareNums {
    row1: Row
    row2: Row
    row3: Row
}

interface Row {
    col1: number
    col2: number
    col3: number
}

const squareNums: SquareNums = ref({
    row1: { col1: 1, col2: 2, col3: 3 },
    row2: { col1: 4, col2: 5, col3: 6 },
    row3: { col1: 7, col2: 8, col3: 9 }
})

const n = ref(0)

const isPerfectSquare = (squareNum: SquareNums) => {
    const row1 = squareNum.row1.col1 + squareNum.row1.col2 + squareNum.row1.col3
    const row2 = squareNum.row2.col1 + squareNum.row2.col2 + squareNum.row2.col3
    const row3 = squareNum.row3.col1 + squareNum.row3.col2 + squareNum.row3.col3

    const col1 = squareNum.row1.col1 + squareNum.row2.col1 + squareNum.row3.col1
    const col2 = squareNum.row1.col2 + squareNum.row2.col2 + squareNum.row3.col2
    const col3 = squareNum.row1.col3 + squareNum.row2.col3 + squareNum.row3.col3

    const diag1 = squareNum.row1.col1 + squareNum.row2.col2 + squareNum.row3.col3
    const diag2 = squareNum.row1.col3 + squareNum.row2.col2 + squareNum.row3.col1

    return row1 === row2 && row2 === row3 && row3 === col1 && col1 === col2 && col2 === col3 && col3 === diag1 && diag1 === diag2
}

</script>

<template>
    <Box
    :margin="2"
    width="100%"
    :maxWidth="50"
    justifyContent="center"
    alignItems="center"
    flexDirection="column"
    borderColor="yellowBright"
    borderStyle="round"
    >
        <Box flexDirection="row">
            <Input v-model="n" />
            <Box :padding="1" borderStyle="round" borderColor="yellowBright">   <Text>{{ squareNums.row1.col2 }}</Text> </Box> 
            <Box :padding="1" borderStyle="round" borderColor="yellowBright"> <Text>{{ squareNums.row1.col3 }}</Text> </Box> 
        </Box>
        <Box flexDirection="row">
            <Box :padding="1" borderStyle="round" borderColor="yellowBright"> <Text>{{ squareNums.row2.col1 }}</Text> </Box> 
            <Box :padding="1" borderStyle="round" borderColor="yellowBright"> <Text>{{ squareNums.row2.col2 }}</Text> </Box> 
            <Box :padding="1" borderStyle="round" borderColor="yellowBright"> <Text>{{ squareNums.row2.col3 }}</Text> </Box> 
        </Box>
        <Box flexDirection="row">
            <Box :padding="1" borderStyle="round" borderColor="yellowBright"> <Text>{{ squareNums.row3.col2 }}</Text> </Box>
            <Box :padding="1" borderStyle="round" borderColor="yellowBright"> <Text>{{ squareNums.row3.col3 }}</Text></Box>
            <Box :padding="1" borderStyle="round" borderColor="yellowBright"> <Text>{{ squareNums.row3.col1 }}</Text> </Box>
        </Box>

    </Box>

    <Text justifyContent="center"  alignItems="center" :color="isPerfectSquare(squareNums) ? 'green' : 'red'" bold>{{ 
        isPerfectSquare(squareNums) ? 'Perfect Square' : 'Not a Perfect Square'
    }}</Text>   
</template>