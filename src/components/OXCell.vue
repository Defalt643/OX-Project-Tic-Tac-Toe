<template>
  <div
    @click="clickCell"
    :class="{
      cell: ture,
      cellX: player === 'X',
      cellO: player === 'O',
      grade: grade
    }"
  >
    {{ player }}
  </div>
</template>
<script>
export default {
  props: ['player', 'row', 'col', 'grade'],
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
<style>
.cell {
  font-size: 30pt;
}
.cellX {
  color: blue;
}
.cellO {
  color: red;
}
.grade {
  background-color: yellow;
}
</style>
