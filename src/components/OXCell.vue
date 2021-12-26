<template>
  <div @click="clickCell">{{ player }}</div>
</template>
<script>
export default {
  props: ['player', 'row', 'col'],
  methods: {
    clickCell (event) {
      // console.log(event)
      // console.log('click' + this.row + ' ' + this.col)
      if (this.player !== '-') return
      this.$emit('cell-click', this.row, this.col)
    }
  }
}
</script>
<style></style>
