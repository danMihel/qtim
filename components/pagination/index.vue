<template>
  <div class="pagination">
    <div class="page-buttons">
      <button v-if="currentPage > 1" class="arrow-button" @click="showPreviousPageBlock">
        <arrov class="back-arrov"/>
      </button>
      <button v-for="pageNumber in visiblePageNumbers" :key="pageNumber" @click="setCurrentPage(pageNumber)"
        :class="{ active: pageNumber === currentPage }">
        {{ pageNumber }}
      </button>
      <button v-if="totalPages > currentPage" class="arrow-button" @click="showNextPageBlock">
        <arrov/>
      </button>
    </div>

  </div>
</template>

<script setup lang="ts">
import { ref, computed, watch, defineProps, defineEmits } from 'vue';
import { useRoute, useRouter } from 'vue-router';
import arrov from '@/public/img/vector.vue'

interface Props {
  currentPage: number;
  totalPages: number;
}

const emit = defineEmits(['update:currentPage']);
const props = defineProps<Props>();
const route = useRoute();
const router = useRouter();

const currentPage = ref(props.currentPage);
const totalPages = computed(() => props.totalPages);

const visiblePageNumbers = computed(() => {
  const currentPageValue = currentPage.value;
  const totalPagesValue = totalPages.value;
  const pageNumbersToShow = 5;
  const pageNumbersBeforeAndAfter = Math.floor(pageNumbersToShow / 2);

  let startPage = currentPageValue - pageNumbersBeforeAndAfter;
  let endPage = currentPageValue + pageNumbersBeforeAndAfter;

  if (startPage < 1) {
    startPage = 1;
    endPage = Math.min(pageNumbersToShow, totalPagesValue);
  }

  if (endPage > totalPagesValue) {
    startPage = Math.max(1, totalPagesValue - pageNumbersToShow + 1);
    endPage = totalPagesValue;
  }

  return Array(endPage - startPage + 1)
    .fill(0)
    .map((_, index) => startPage + index);
});

const setCurrentPage = (pageNumber: number): void => {
  currentPage.value = pageNumber;
  emit('update:currentPage', pageNumber);
  router.push({ query: { ...route.query, page: pageNumber.toString() } });
};

const showNextPageBlock = (): void => {
  const currentPageValue = currentPage.value;
  const totalPagesValue = totalPages.value;
  if (currentPageValue < totalPagesValue) {
    setCurrentPage(currentPageValue + 1);
  }
};
const showPreviousPageBlock = (): void => {
  const currentPageValue = currentPage.value;
  if (currentPageValue > 1) {
    setCurrentPage(currentPageValue - 1);
  }
};
watch(() => props.currentPage, (newValue) => {
  currentPage.value = newValue;
});
onBeforeMount(() => {
  const pageNumberQuery = Number(route.query.page);
  if(!pageNumberQuery) return 
  setCurrentPage(pageNumberQuery);
});
</script>

<style lang="scss" scoped>
.pagination {
  display: flex;
  gap: 8px;
  margin-top: 16px;
  overflow: hidden;

  .page-buttons {
    display: flex;
    gap: 8px;
    margin-right: auto;
    /* Добавлено для выравнивания кнопок справа */
  }

  button {
    width: 44px;
    height: 44px;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    font-size: 16px;
    line-height: 8px;
    background-color: rgba(243, 243, 243, 1);
    color: rgba(16, 16, 16, 1);

    &.active {
      background-color: rgba(16, 16, 16, 1);
      color: rgba(255, 255, 255, 1);
    }
  }

  .arrow-button {
    width: 44px;
    height: 44px;
    border-radius: 12px;
    cursor: pointer;
    font-size: 16px;
    line-height: 8px;
    background-color: transparent;
    border: 1px solid rgba(232, 232, 232, 1);
    color: rgba(16, 16, 16, 1);
    .back-arrov{
      transform: rotate(180deg);
    }
  }
}
</style>