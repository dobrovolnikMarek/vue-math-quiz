<template>
  <div>
    <button @click="$emit('changeOperator', '+')"><p>
      Addition
      <br />+</p>
    </button>
    <button @click="$emit('changeOperator', '-')"><p>
      Subtraction
      <br />-</p>
    </button>
    <button @click="$emit('changeOperator', '/')"><p>
      Division
      <br />/</p>
    </button>
    <button @click="$emit('changeOperator', '*')">
     <p> Multiplication
      <br />*
     </p>    </button>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>