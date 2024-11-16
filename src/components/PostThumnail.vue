<script setup>
import { computed, ref } from "vue";

const props = defineProps({
  title: String,
  subtitle: String,
  img: String,
  index: Number,
});

const isHovering = ref(false);

const onMouseOver = () => {
  isHovering.value = true;
};

const onMouseOut = () => {
  isHovering.value = false;
};

const leftMargin = computed(() => {
  if (props.index % 2 === 0) {
    return "lg:ml-auto";
  }
});
</script>

<template>
  <div
    class="mx-auto lg:mx-0 relative hover:cursor-pointer overflow-hidden img-container img-gradient"
    :class="leftMargin"
    @mouseover="onMouseOver"
    @mouseout="onMouseOut"
  >
    <div
      class="w-full absolute bottom-0 left-0 z-40 transition-all ease-in-out duration-500 img-gradient"
      :class="isHovering ? 'px-3 pb-3 pt-10' : 'px-5 pb-5 pt-8'"
    >
      <h1
        class="text-white font-semibold text-balance transition-all ease-in-out duration-500 z-50"
        :class="isHovering ? 'text-2xl' : 'text-xl'"
      >
        {{ title }}
      </h1>
      <h2 class="text-white text-balance z-50">{{ subtitle }}</h2>
    </div>

    <img
      class="max-h-full transition-all ease-in-out duration-500 img-container"
      :class="{ 'scale-110': isHovering }"
      :src="img"
      :alt="title"
      width="415"
      height="236"
    />
  </div>
</template>

<style scoped>
.img-container {
  @media screen and (min-width: 500px) {
    max-width: 415px;
    max-height: 236px;
  }
}

.img-gradient {
  background: linear-gradient(transparent, #000);
}
</style>
