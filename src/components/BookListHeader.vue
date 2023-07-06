<template>
  <div class="header gray-1">
    <span>title</span>
    <span>published</span>
    <span>rank</span>
    <span>buy on</span>
  </div>
</template>

<script setup lang="ts"></script>

<style scoped lang="scss">
.header {
  display: grid;
  grid-template-columns: 4fr 1fr 1fr 1fr;
  text-align: center;
  text-transform: uppercase;
  font-weight: bold;
  padding: 20px 30px;

  > *:nth-child(1) {
    text-align: left;
  }
}
</style>
