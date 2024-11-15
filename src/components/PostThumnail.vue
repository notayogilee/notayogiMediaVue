<script setup>
import { computed } from "vue";

const props = defineProps({
  title: String,
  subtitle: String,
  img: String,
  index: Number,
});

const leftMargin = computed(() => {
  if (props.index % 2 === 0) {
    return "lg:ml-auto";
  }
});
</script>

<template>
  <div
    class="mx-auto lg:mx-0 relative hover:cursor-pointer overflow-hidden img-container"
    :class="leftMargin"
  >
    <div class="absolute bottom-5 left-5">
      <h1 class="text-white">{{ title }}</h1>
      <h2 class="text-white">{{ subtitle }}</h2>
    </div>

    <img
      class="object-cover max-h-full hover:scale-110 transition ease-in-out duration-500 img-container"
      :src="img"
      :alt="title"
      width="415"
      height="236"
    />
  </div>
</template>

<style scoped>
@media screen and (min-width: 500px) {
  .img-container {
    max-width: 415px;
    max-height: 236px;
  }
}
</style>
