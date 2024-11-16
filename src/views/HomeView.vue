<script setup>
import client, { urlFor } from "../sanity/client";
import { ref, onBeforeMount } from "vue";
import PostThumbnail from "../components/PostThumnail.vue";
import TheCarousel from "@/components/TheCarousel.vue";

const posts = ref([]);
const carouselPosts = ref([]);

async function getAllPosts() {
  const query = '*[_type == "post"]';
  try {
    const data = await client.fetch(query);
    posts.value = data;
    getCarouselPosts();
  } catch (error) {
    console.error("Query failed: ", error);
  }
}

function getCarouselPosts() {
  // Get last 3 last posts created
  const sortedByCreateAt = posts.value.sort(
    (postA, postB) => postB._createdAt - postA._createdAt
  );
  console.log("SORTED: ", sortedByCreateAt);
  const threeRecentPosts = sortedByCreateAt.slice(0, 3);
  console.log(threeRecentPosts);
}

onMounted: getAllPosts();
</script>

<template>
  <main class="container mx-auto p-10">
    <TheCarousel :carouselPosts="carouselPosts" />
    <ul class="grid lg:grid-rows-2 grid-flow-row lg:grid-cols-2 gap-5">
      <li
        class="w-100"
        v-for="({ title, subtitle, image, _id }, index) in posts"
        :key="_id"
      >
        <PostThumbnail
          :title="title"
          :subtitle="subtitle"
          :img="urlFor(image).url()"
          :index="index"
        />
      </li>
    </ul>
  </main>
</template>
