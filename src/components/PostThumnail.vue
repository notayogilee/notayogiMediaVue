<script setup>
import { computed } from "vue";

const props = defineProps({
  title: String,
  subtitle: String,
  img: String,
});

// const backgroundImage = computed(() => {
//   return {
//     "--background-image": `url(${props.img.options.baseUrl}/images/${props.img.options.projectId}/${dataset}/${source})`,
//   };
// });
</script>

<template>
  <div class="relative hover:cursor-pointer overflow-hidden">
    <div class="absolute bottom-5 left-5">
      <h1 class="text-white">{{ title }}</h1>
      <h2 class="text-white">{{ subtitle }}</h2>
    </div>

    <img
      class="w-full h-full object-cover hover:scale-110 transition ease-in-out duration-500"
      :src="img"
      alt="title"
    />
  </div>
</template>
