<script setup>
import client, { urlFor } from "../sanity/client";
import { ref, onBeforeMount } from "vue";
import PostThumbnail from "../components/PostThumnail.vue";

const posts = ref([]);

async function getAllPosts() {
  const query = '*[_type == "post"]';
  try {
    const data = await client.fetch(query);
    console.log(data);
    posts.value = data;
  } catch (error) {
    console.error("Query failed: ", error);
  }
}

onMounted: getAllPosts();
</script>

<template>
  <main class="container mx-auto p-10">
    <ul class="grid lg:grid-rows-2 grid-flow-row lg:grid-cols-2 gap-5">
      <li
        class="w-100"
        v-for="({ title, subtitle, image, _id }, index) in posts"
        :key="_id"
      >
        <PostThumbnail
          :title="title"
          :subtitle="subtitle"
          :img="urlFor(image.asset._ref)"
          :index="index"
        />
      </li>
    </ul>
  </main>
</template>
