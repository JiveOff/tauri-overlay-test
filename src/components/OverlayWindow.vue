<template>
  <div class="box">
    <div class="box-header">
      <slot name="header" />
    </div>
    <div class="box-content">
      <slot />
    </div>
  </div>
</template>

<script setup lang="ts"></script>

<style lang="scss">
.box {
  width: 300px;
  height: 200px;

  background-color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;

  border-radius: 0.5rem;

  .box-header {
    background-color: white;
    padding: 1rem;
    border-radius: 0.5rem;

    h1 {
      margin: 0;
      line-height: 10px;
    }
  }

  .box-content {
    padding: 1rem;
    border-radius: 0.5rem;
  }
}
</style>
