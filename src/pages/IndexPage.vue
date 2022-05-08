<template>
  <q-carousel
    v-if="photos.length > 0"
    animated
    v-model="slide"
    infinite
    :autoplay="speedMs"
    height="100vh"
    :swipeable="true"
    transition-prev="slide-right"
    transition-next="slide-left"
    @mouseenter="speedMs = false"
    @mouseleave="speedMs = 600_000"
  >
    <q-carousel-slide
      v-for="photo in photos"
      :key="photo.asset_id"
      :name="Number(photo.context.custom.index)"
      :img-src="photo.secure_url"
    />
  </q-carousel>
</template>

<script lang="ts">
import { Image, RequestResponse } from 'src/assets/responses.types';
import { defineComponent, ref, watchEffect } from 'vue';
import { useFetch } from '@vueuse/core';

export default defineComponent({
  setup() {
    const slide = ref(0);
    const speedMs = ref<number | boolean>(600_000); // Every Ten minutes
    const refetchTimeout = 60_000; // Each Minute
    const photos = ref<Image[]>([]);

    async function fetchPhotos(): Promise<void> {
      const { data } = await useFetch(
        'https://photoframe-admin.netlify.app/.netlify/functions/fetch-photos'
      ).json<RequestResponse>();

      watchEffect(() => {
        if (data) {
          photos.value =
            data.value?.resources.sort(
              (a, b) =>
                Number(a.context.custom.index) - Number(b.context.custom.index)
            ) || [];
        }
        console.log({ photos: photos.value });
      });
    }

    //Every minute refresh photo list
    setInterval(fetchPhotos, refetchTimeout);
    fetchPhotos();

    return {
      slide,
      photos,
      speedMs,
    };
  },
});
</script>
