<template>
  <herder class="container">
    <div class="flex bg-white border-b-4 border-b-neutral-900">
      <div class="flex-none w-72 h-14"></div>
      <div class="grow h-14 flex justify-between items-center">
        <h1 class="text-3xl">MetaWall</h1>
        <div class="flex items-center space-x-2">
          <div class="rounded-full">
            <img
              width="30"
              src="../src/assets/image/user.png"
              alt="User"
            >
          </div>
          <p class="text-xl border-b-2 border-black user">Member </p>
        </div>
      </div>
      <div class="flex-none w-72 h-14"></div>
    </div>
  </herder>
  <main class="mt-10">
    <div class="flex">
      <div class="flex-none w-72 h-14"></div>
      <div class="grow flex">
        <article class="w-2/3 mr-7">
          <router-view />
        </article>
        <aside class="w-1/3">
          <ul class="aside">
            <li>
              <button class="btn-add-article" @click="$router.push('/Create')">張貼動態</button>
            </li>
            <li class="flex items-center">
              <img
                class="w-12 h-12"
                src="../src/assets/image/user.png"
                alt="頭像"
              >
              <p class="ml-4">{{ user.data.name }}</p>
            </li>
            <li class="flex items-center">
              <div class="icon">
                <img
                  src="../src/assets/image/bell.png"
                  alt="追蹤名單"
                  width="22"
                >
              </div>
              <p class="ml-4">追蹤名單</p>
            </li>
            <li class="flex items-center">
              <div class="icon">
                <img
                  src="../src/assets/image/like.png"
                  alt="按讚的文章"
                  width="22"
                >
              </div>
              <p class="ml-4">我按讚的文章</p>
            </li>
          </ul>
        </aside>
      </div>
      <div class="flex-none w-72 h-14"></div>
    </div>
  </main>
</template>

<script>
import { reactive } from 'vue';
import axios from 'axios';

export default {
  setup() {
    const user = reactive({ data: {} });
    async function getUser() {
      try {
        const { data } = await axios.get(`${process.env.VUE_APP_APIPATH}/users`);
        user.data = data;
      } catch (error) {
        alert('user有錯誤');
      }
    }
    getUser();
    return { user };
  },
};
</script>

<style lang="scss">
body {
  background: url('../src/assets/image/bg.png');
  font-family: 'Noto Sans TC', sans-serif;
}
h1 {
  font-family: 'Paytone One', sans-serif;
  font-size: 8rem;
}
.user {
  font-family: 'Azeret Mono', monospace;
  font-weight: 600;
}
.btn-add-article {
  box-shadow: -2px 2px 0px #000400;
  @apply block w-full py-4 rounded-lg bg-blue-900 border-2 border-neutral-900 text-white text-base;
}
.aside {
  min-height: 336px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  @apply py-8 px-6 bg-white border-2 border-neutral-900;
}
.icon {
  @apply flex justify-center items-center rounded-full w-12 h-12 border-2
  border-neutral-900 bg-sky-200;
}
</style>
