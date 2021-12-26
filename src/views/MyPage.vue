<template>
  <div>
      <h1>
          MyPage
      </h1>
      <h3>
          {{ $route.params.name }}
          {{ name }}
      </h3>
      <img src="../assets/jarnDang.jpg" alt="">
  </div>
</template>
<script>
export default {
  props: ['name']
}
</script>
<style></style>
