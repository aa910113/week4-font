<template>
<ul class="displat-article">
  <li class="article" v-if="articles.data.length === 0">
    <div class="border-b-2 border-neutral-900 px-4 py-5">
      <ul class="flex">
        <li class="w-2.5 h-2.5 mr-1.5 bg-red-600 rounded-full border border-neutral-900"></li>
        <li class="w-2.5 h-2.5 mr-1.5 bg-yellow-500 rounded-full border border-neutral-900"></li>
        <li class="w-2.5 h-2.5 mr-1.5 bg-lime-500 rounded-full border border-neutral-900"></li>
      </ul>
    </div>
    <div class="flex justify-center items-center h-20">
      <p class="text-zinc-500">目前尚無動態，新增一則貼文吧！</p>
    </div>
  </li>
  <li
    class="article p-6"
    v-else
    v-for="article in articles.data"
    :key="article._id"
  >
    <div class="article-header">
      <ul class="flex items-center">
        <li class="w-11">
          <img src="../assets/image/user@2x.png" alt="avatar">
        </li>
        <li class="ml-4">
          <p class="font-black">{{ article.name }}</p>
          <p class="text-xs text-zinc-500">
            {{ article.date.substring(0, 10) }}
            {{ article.date.substring(11, 19) }}
          </p>
        </li>
      </ul>
    </div>
    <div class="my-4">
      <p>{{ article.message }}</p>
    </div>
    <div class="article-image">
      <img :src="article.photo" alt="">
    </div>
  </li>
</ul>
</template>

<script>
import { reactive } from 'vue';
import axios from 'axios';

export default {
  name: 'HomeView',
  setup() {
    const articles = reactive({ data: [] });
    async function getAllarticle() {
      try {
        const { data } = await axios.get(`${process.env.VUE_APP_APIPATH}/article`);
        articles.data = data;
      } catch (error) {
        alert('user有錯誤');
      }
    }
    getAllarticle();
    return { articles };
  },
};
</script>

<style lang="scss">
.displat-article{
  height: 75vh;
  overflow: auto;
  scrollbar-width: none;
  -ms-overflow-style: none;
}
.displat-article::-webkit-scrollbar {
  display: none;
}
.article{
  box-shadow: 0px 3px 0px #000400;
  @apply mb-4 bg-white border-2 border-neutral-900 rounded-lg
}
</style>
