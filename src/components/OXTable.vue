<template>
  <div>
    <div v-if="finish">
      <!-- <span v-if="winner !== '-'">{{ winner }} Win!!!</span>
      <span v-else>Draw !!!</span> -->
      <span>{{ result }}</span>
      <button @click="newGame">New Game</button>
    </div>
    <div v-else>{{ turn }} Trun...</div>
    <table>
      <tr v-for="(line, lineId) in table" :key="lineId">
        <td v-for="(item, itemId) in line" :key="itemId">
          <OXCell
            :player="item"
            :row="lineId"
            :col="itemId"
            :grade="gradeTable[lineId][itemId]"
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
      count: 0,
      finish: false,
      winner: '-',
      gradeTable: [
        [false, false, false],
        [false, false, false],
        [false, false, false]
      ],
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
  mounted () {
    this.randomPlayer()
  },
  computed: {
    result () {
      // if (this.finish && this.winner === '-') {
      //   return 'Draw'
      // } else {
      //   return this.turn + ' Win!!!'
      // }

      return this.finish && this.winner === '-'
        ? 'Draw!!!'
        : this.turn + ' Win!!!'
    }
  },
  methods: {
    newGame () {
      this.count = 0
      this.winner = '-'
      this.finish = false
      this.initTable()
      this.randomPlayer()
    },
    initTable () {
      for (let row = 0; row < 3; row++) {
        for (let col = 0; col < 3; col++) {
          this.table[row][col] = '-'
          this.gradeTable[row][col] = false
        }
      }
    },
    cellClick (row, col) {
      console.log('Cell click ' + row + ' ' + col)
      this.table[row][col] = this.turn
      this.count++
      if (this.checkWin(row, col)) {
        console.log('Win')
        this.finish = true
        this.winner = this.turn
        return
      }
      if (this.count === 9) {
        this.finish = true
      }
      this.switchTurn()
    },
    switchTurn () {
      if (this.turn === 'O') {
        this.turn = 'X'
      } else {
        this.turn = 'O'
      }
    },
    randomPlayer () {
      console.log(Math.floor(Math.random() * 100) % 2)
      if (Math.floor(Math.random() * 100) % 2 === 0) {
        this.turn = 'O'
      } else {
        this.turn = 'X'
      }
    },
    checkRow (row) {
      for (let col = 0; col < 3; col++) {
        if (this.table[row][col] !== this.turn) {
          return false
        }
      }
      for (let col = 0; col < 3; col++) {
        this.gradeTable[row][col] = true
      }
      return true
    },
    checkCol (col) {
      for (let row = 0; row < 3; row++) {
        if (this.table[row][col] !== this.turn) {
          return false
        }
      }
      for (let row = 0; row < 3; row++) {
        this.gradeTable[row][col] = true
      }
      return true
    },
    checkX1 () {
      for (let index = 0; index < 3; index++) {
        if (this.table[index][index] !== this.turn) {
          return false
        }
      }
      for (let index = 0; index < 3; index++) {
        this.gradeTable[index][index] = true
      }
      return true
    },
    checkX2 () {
      for (let index = 0; index < 3; index++) {
        if (this.table[index][2 - index] !== this.turn) {
          return false
        }
      }
      for (let index = 0; index < 3; index++) {
        this.gradeTable[index][2 - index] = true
      }
      return true
    },
    checkWin (row, col) {
      if (
        this.checkRow(row) ||
        this.checkCol(col || this.checkX1() || this.checkX2())
      ) {
        return true
      } else {
        return false
      }
    }
  }
}
</script>
<style>
table {
  margin-left: auto;
  margin-right: auto;
  border: 1pt solid black;
}
td {
  text-align: center;
  vertical-align: middle;
  width: 50pt;
  height: 50pt;
}
</style>
