<template>
  <div class="cell sum-cell"
    :class="{'solved': current == expected}"
    :title="current">
    {{ expected }}
  </div>

</template>

<script>
export default {
  props: ['expected', 'current']
}

</script>

<style scoped>
  .cell {
    width: 45px;
    text-align: center;
    margin: 5px;
    border-radius: 50%;
    border: 1px solid grey;
    line-height: 40px;
  }
  .sum-cell {
    background-color: white;
  }
  .sum-cell.solved {
    border-color: green !important;
    background-color: coral;
  }
</style>
