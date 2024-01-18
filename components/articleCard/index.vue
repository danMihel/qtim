<template>
  <div class="preview" @mouseover="handleMouseOver" @mouseleave="handleMouseLeave">
    <div class="img-wrapper">
      <NuxtLink :to="`/article/${articleData.id}`"> <img :src="imageSource" :alt="altText"></NuxtLink>
    </div>
    <p class="description">{{ articleData.description }}</p>
    <p class="more" v-if="state.showMore"> 
      <NuxtLink :to="`/article/${articleData.id}`">Read more</NuxtLink>
    </p>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';

interface ArticleData {
  image: string;
  description: string;
  id: string;
}

const props = defineProps<{articleData: ArticleData;}>();

const imageSource = ref<string>(props.articleData.image);
const parts = imageSource.value.split('/');
const altText = parts[parts.length - 1];


const state = reactive({
  showMore: false,
});

function handleMouseOver(): void {
  state.showMore = true;
}

function handleMouseLeave(): void {
  state.showMore = false;
}
</script>

<style lang="scss" scoped>
.preview {
  max-width: 280px;
  font-size: 24px;
  line-height: 20px;

  .img-wrapper {
    min-height: 200px;
  }

  img {
    width: 100%;
  }

  .description {
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 3;
  }

  .more {
    opacity: 0;
    color: rgba(226, 190, 255, 1);
    cursor: pointer;
  }

  &:hover {
    position: absolute;
    transform: translateY(-28px);
    transition: transform 0.3s;

    .more {
      opacity: 1;
      transition: opacity 0.3s;
    }
  }
}</style>