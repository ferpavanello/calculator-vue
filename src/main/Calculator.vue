<template>
  <div class="calculator">
    <Display :value="displayValue" />
    <Button label="C" triple @onClick="clearMemory" />
    <Button label="/" operation  @onClick="setOperation" />
    <Button label="7" @onClick="addDigit" />
    <Button label="8" @onClick="addDigit" />
    <Button label="9" @onClick="addDigit" />
    <Button label="*" operation @onClick="setOperation" />
    <Button label="4" @onClick="addDigit" />
    <Button label="5" @onClick="addDigit" />
    <Button label="6" @onClick="addDigit" />
    <Button label="-" operation @onClick="setOperation" />
    <Button label="1" @onClick="addDigit" />
    <Button label="2" @onClick="addDigit" />
    <Button label="3" @onClick="addDigit" />
    <Button label="+" operation @onClick="setOperation" />
    <Button label="0" double @onClick="addDigit" />
    <Button label="." @onClick="addDigit" />
    <Button label="=" operation @onClick="setOperation" />
  </div>
</template>

<script>
import Display from '../components/Display'
import Button from '../components/Button'

export default {
  components: {
    Button,
    Display
  },
  data () {
    return {
      displayValue: '0',
      clearDisplay: false,
      operation: null,
      values: [0, 0],
      current: 0
    }
  },
  methods: {
    clearMemory () {
      Object.assign(this.$data, this.$options.data())
    },
    setOperation (operation) {
      if (this.current === 1) {
        const wasEqualPressed = operation === '='
        const currentOperation = this.operation

        this.values[0] = eval(
          `${this.values[0]} ${currentOperation} ${this.values[1]}`
        )
        this.values[1] = 0

        this.displayValue = this.values[0]
        this.operation = wasEqualPressed ? null : operation
        this.current = wasEqualPressed ? 0 : 1

        this.clearDisplay = !wasEqualPressed
        return
      }

      if (operation === '=') {
        this.clearMemory()
      } else {
        this.operation = operation
        this.current = 1
        this.clearDisplay = true
      }
    },
    addDigit (n) {
      const isDot = n === '.'
      if (isDot && this.displayValue.includes('.')) {
        return
      }

      const shouldClean = (this.displayValue === '0' && !isDot) || this.clearDisplay
      const currentValue = shouldClean ? '' : this.displayValue
      const displayValue = currentValue + n
      
      this.displayValue = displayValue
      this.clearDisplay = false

      if (!isDot) {
        const i = this.current
        const newValue = parseFloat(displayValue)
        this.values[i] = newValue
      }
    }
  }
}
</script>

<style>
  .calculator {
    height: 320px;
    width: 235px;
    border-radius: 5px;
    overflow: hidden;

    display: grid;
    grid-template-columns: repeat(4, 25%);
    grid-template-rows: 1fr repeat(5, 48px);
  }
</style>