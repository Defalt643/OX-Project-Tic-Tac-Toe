<template>
  <div>
    <table>
      <tr v-for="(line, lineId) in table" :key="lineId">
        <td v-for="(item, itemId) in line" :key="itemId">{{ item }}</td>
      </tr>
    </table>
  </div>
</template>
<script>
export default {
  data () {
    return {
      table: [
        ['-', '-', '-'],
        ['-', '-', '-'],
        ['-', '-', '-']
      ]
    }
  }
}
</script>
<style></style>
