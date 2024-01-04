<template>
  <div>
    <h1>トップページ</h1>
    <hr />
    <ul>
      <li v-for="post in posts" :key="post.id">
        {{ post.title }}
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { useAsyncData } from "nuxt/app";
import type { Post } from "@/types/post";

const { data: posts } = useAsyncData<Post[]>(async () => {
  const response = await fetch("http://backend-web-1:3000/posts");
  if (!response.ok) throw new Error("Failed to fetch posts");
  return await response.json();
});
</script>
