<template>
  <div>
    <table>
      <tr v-for="(line, lineId) in table" :key="lineId">
        <td v-for="(item, itemId) in line" :key="itemId">
          <OXCell
            :player="item"
            :row="lineId"
            :col="itemId"
            @cell-click="cellClick"
          />
        </td>
      </tr>
    </table>
  </div>
</template>
<script>
import OXCell from './OXCell.vue'
export default {
  data () {
    return {
      turn: 'O',
      table: [
        ['-', '-', '-'],
        ['-', '-', '-'],
        ['-', '-', '-']
      ]
    }
  },
  components: {
    OXCell
  },
  methods: {
    cellClick (row, col) {
      console.log('Cell click ' + row + ' ' + col)
      this.table[row][col] = this.turn
    }
  }
}
</script>
<style></style>
