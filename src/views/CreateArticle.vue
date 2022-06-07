<template>
  <div class="relative">
    <div class="mb-4 bg-white border-2 border-neutral-900 absolute w-full top-1 right-1">
      <div class="flex justify-center items-center h-20">
      </div>
    </div>
  </div>
  <ul class="relative">
    <li class="mb-4 bg-white border-2 border-neutral-900">
      <div class="flex justify-center items-center h-20">
        <p class="text-xl font-extrabold">張貼動態</p>
      </div>
    </li>
    <li class="add-article">
      <label for="articleContent">
        <p>文章內容</p>
        <textarea
          id="articleContent"
          class="border-2 border-neutral-900 w-full p-3"
          placeholder="輸入您的貼文內容"
          cols="30"
          rows="10"
          v-model="article.message"
        ></textarea>
      </label>
      <label for="uploadFile">
        <span class="my-4 rounded bg-black text-white py-1 px-8">上傳照片</span>
        <input
          id="uploadFile"
          type="file"
          @change="handleFileUpload"
          style="display: none;"
        >
      </label>
      <img
        class="mt-3"
        v-if="image"
        :src="image"
        alt="文章圖片"
      >
      <div class="text-center">
        <button
          class="
          flex
          mt-8
          font-semibold
          rounded
          border-2
          border-black
          bg-gray-400
          py-4
          px-32"
          @click="createArticle"
        >
          <svg
            class="animate-spin -ml-1 mr-3 h-5 w-5 text-white"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 24 24"
            v-show="loading"
          >
            <circle
              class="opacity-25"
              cx="12"
              cy="12"
              r="10"
              stroke="currentColor"
              stroke-width="4"
            ></circle>
            <path
              class="opacity-75"
              fill="currentColor"
              d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042
              1.135 5.824 3 7.938l3-2.647z"
            ></path>
          </svg>
          送出貼文
        </button>
      </div>
    </li>
  </ul>
</template>

<script>
import { ref, reactive } from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';

export default {
  setup() {
    const router = useRouter();
    const article = reactive({
      name: 'Daniel',
      userId: '628d0b89c32e7b686cb9b1f3',
      message: '',
      photo: '',
    });
    let file = {};
    const image = ref('');
    const handleFileUpload = (event) => {
      try {
        [file] = event.target.files;
        const reader = new FileReader();
        reader.addEventListener('load', (e) => {
          image.value = e.target.result;
        });
        reader.readAsDataURL(file);
      } catch (error) {
        console.log(error);
      }
    };
    const createArtucle = async () => {
      try {
        const formData = new FormData();
        formData.append('image', file);
        formData.append('type', 'file');
        const { data } = await axios.post(
          'https://api.imgur.com/3/image',
          formData,
          {
            headers: {
              Authorization: 'Bearer 78a149bc21f3e2977b838f68c293d82cfb9a5985',
            },
          },
        );
        console.log(data);
      } catch (error) {
        console.log(error);
      }
    };
    const loading = ref(false);
    const createArticle = async () => {
      try {
        loading.value = true;
        const formData = new FormData();
        formData.append('userId', article.userId);
        formData.append('name', article.name);
        formData.append('message', article.message);
        formData.append('image', file);
        const { data } = await axios.post(
          `${process.env.VUE_APP_APIPATH}/article`,
          formData,
        );
        if (data.status === 'success') {
          router.push({
            path: '/',
          });
        }
      } catch (error) {
        console.log(error);
      } finally {
        loading.value = false;
      }
    };
    return {
      article,
      handleFileUpload,
      file,
      image,
      createArtucle,
      createArticle,
      loading,
    };
  },
};
</script>

<style lang="scss">
.add-article {
  box-shadow: 0px 3px 0px #000400;
  @apply mb-4 p-8 bg-white border-2 border-neutral-900 rounded-lg;
}
</style>
