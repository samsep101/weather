<template>
  <div class="card">
    <slot></slot>
  </div>
</template>
<script lang="ts" setup>

defineOptions({
  name: 'Card',
});

</script>
<style scoped>
.card {
  width: 100%;
  padding: 16px;
  background: rgba(244, 244, 245, 0.8);
  border-radius: 12px;
}

.card--white {
  background: #ffffff;
}

</style>
