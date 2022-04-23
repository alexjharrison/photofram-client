<template>
  <router-view v-if="hasStarted" />
  <div
    class="flex full-height full-width row justify-center items-center"
    v-else
  >
    <q-btn
      color="primary"
      @click="handleStart"
      label="Click to Start Slideshow"
      size="xl"
    />
  </div>
</template>

<script lang="ts">
import { useQuasar } from 'quasar';
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'App',
  setup() {
    const hasStarted = ref(false);
    const $q = useQuasar();

    function handleStart() {
      // Requesting fullscreen mode:
      $q.fullscreen
        .request()
        .then(() => {
          hasStarted.value = true;
        })
        .catch((err) => {
          console.log(err);
        });
    }

    return { hasStarted, handleStart };
  },
});
</script>

<style lang="scss" scoped></style>
