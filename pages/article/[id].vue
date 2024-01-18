<template>
  <div class="wrapper">
    <div class="spinner" v-if="showSpinner">
      <spinner />
    </div>
    <div v-if="!showSpinner" class="post-wraper">
      <titleH2>{{ post?.title }}</titleH2>
      <div class="img-wrapper">
        <img :src="post?.image">
      </div>
      <p class="subtitle">About</p>
      <p class="description">{{ post?.description }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useRoute } from 'vue-router';
import { onMounted, ref } from 'vue';
import titleH2 from '@/components/UI/titleH2';
import spinner from '@/components/UI/spinner'

interface Post {
  id: string;
  title: string;
  image: string;
  description: string;
}

let showSpinner = ref(false);
const route = useRoute();
const post = ref<Post | null>(null);

async function fetchPost(): Promise<void> {
  try {
    showSpinner.value = true
    const response = await fetch(`https://6082e3545dbd2c001757abf5.mockapi.io/qtim-test-work/posts/${route.params.id}`);
    if (!response.ok) {
      throw new Error('Ошибка при выполнении запроса');
    }

    const data = await response.json();
    showSpinner.value = false
    post.value = data;
  } catch (error) {
    console.error('Произошла ошибка:', error);
  }
}

onMounted(async () => {
  await fetchPost();
});



</script>

<style lang="scss" scoped>
.spinner{
  margin-left: 45vw;
  margin-top: 50px;
}
.post-wraper {
  max-width: 1217px;
  margin: 0 auto;

  .img-wrapper {
    max-width: 1216px;
    max-height: 700px;
    overflow: hidden;
  }

  img {
    width: 100%;
  }

  .subtitle {
    margin-top: 80px;
    font-size: 16px;
    font-weight: 400;
    line-height: 16px;
  }

  .description {
    max-width: 695px;
    font-weight: 400;
    font-size: 36px;
    line-height: 44.64px;
  }
}</style>