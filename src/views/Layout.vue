<template>
  <div class="layout">
    <ul class="flex justify-between mb-4">
      <li class="px-4 py-3 border-2 border-neutral-900 bg-white">
        <select
          class="pr-12"
          name=""
          id=""
        >
          <option value="new">最新貼文</option>
        </select>
      </li>
      <li class="border-2 border-neutral-900 w-full ml-3">
        <label for="s" class="flex h-full">
          <input
            class="w-full pl-4"
            type="search"
            placeholder="搜尋貼文"
            id="s"
          >
          <button class="w-14 bg-blue-900 text-center border-l-2 border-neutral-900">
            <svg
              class="inline"
              xmlns="http://www.w3.org/2000/svg"
              height="24px"
              viewBox="0 0 24 24"
              width="24px"
              fill="#eee"
            >
              <path
                d="M0 0h24v24H0z"
                fill="none"
              />
              <path d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5
              3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49
              19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5
              14z" />
            </svg>
          </button>
        </label>
      </li>
    </ul>
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'LayoutView',
};
</script>

<style lang="scss">
.layout {
  @apply text-base;
}
</style>
