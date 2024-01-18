<template>
  <div class="page-wraper">
    <titleH2>Articles</titleH2>
    <div class="spinner" v-if="showSpinner">
      <spinner />
    </div>
    <div v-if="!showSpinner" class="cardWraper">
      <div v-for="post in displayedPosts" :key="post.id">
        <articleCard :articleData="post" />
      </div>
    </div>
    <Pagination :currentPage="currentPage" :totalPages="totalPages" @update:currentPage="setCurrentPage" />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, computed } from 'vue';
import titleH2 from '@/components/UI/titleH2';
import articleCard from '@/components/articleCard';
import Pagination from '@/components/Pagination';
import spinner from '@/components/UI/spinner'
interface Post {
  id: string;
}
let showSpinner = ref(false);
const itemsPerPage = 8;

async function fetchPosts(): Promise<Post[]> {
  try {
    showSpinner.value = true
    const response = await fetch('https://6082e3545dbd2c001757abf5.mockapi.io/qtim-test-work/posts/');

    if (!response.ok) {
      throw new Error('Ошибка при выполнении запроса');
    }

    const data = await response.json();
    showSpinner.value = false
    return data;
  } catch (error) {
    console.error('Произошла ошибка:', error);
    return [];
  }
}

const posts = ref<Post[]>([]);
const currentPage = ref(1);

onMounted(async () => {
  posts.value = await fetchPosts();
});
const totalPages = computed(() => Math.ceil(posts.value.length / itemsPerPage));
const displayedPosts = computed(() => {
  const startIndex = (currentPage.value - 1) * itemsPerPage;
  const endIndex = startIndex + itemsPerPage;
  return posts.value.slice(startIndex, endIndex);
});

function setCurrentPage(pageNumber: number): void {
  currentPage.value = pageNumber;
}
</script>

<style lang="scss" scoped>
.page-wraper {
  max-width: 1217px;
  margin: 0 auto;

  .spinner {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .cardWraper {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-row-gap: 40px;
    grid-column-gap: 30px;
  }
}</style>