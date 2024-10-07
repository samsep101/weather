<template>
  <template v-if="loading">
    <slot name="loading">
      <div class="loading">
        <Skeleton></Skeleton>
      </div>
    </slot>
  </template>
  <template v-else>
    <slot name="default"/>
  </template>
</template>

<script lang="ts" setup>
import Skeleton from "@/shared/ui/Skeleton/index.vue";

const props = defineProps<{
  loading: boolean;
}>();

defineOptions({
  name: 'SuspenseLoading',
});

</script>

<style lang="scss" scoped>
.loading {
  width: 100%;
  height: 100%;
}
</style>
