<template>
  <q-carousel
    animated
    v-model="slide"
    infinite
    :autoplay="autoplay"
    height="100vh"
    :swipeable="true"
    transition-prev="slide-right"
    transition-next="slide-left"
    @mouseenter="autoplay = false"
    @mouseleave="autoplay = true"
  >
    <q-carousel-slide
      :name="1"
      img-src="https://cdn.quasar.dev/img/mountains.jpg"
    />
    <q-carousel-slide
      :name="2"
      img-src="https://cdn.quasar.dev/img/parallax1.jpg"
    />
    <q-carousel-slide
      :name="3"
      img-src="https://cdn.quasar.dev/img/parallax2.jpg"
    />
    <q-carousel-slide
      :name="4"
      img-src="https://cdn.quasar.dev/img/quasar.jpg"
    />
  </q-carousel>
</template>

<script lang="ts">
// import { Todo, Meta } from 'components/models';
// import ExampleComponent from 'components/ExampleComponent.vue';
import { defineComponent, ref } from 'vue';

export default defineComponent({
  setup() {
    return {
      slide: ref(1),
      autoplay: ref(true),
    };
  },
});
</script>
