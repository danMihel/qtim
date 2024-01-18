<template>
    <button class="normal-btn">
      <slot></slot>
    </button>
  </template>
  <script setup lang="ts">
  </script>
  <style lang="scss" scoped>
  .normal-btn{
    background-color: rgba(16, 16, 16, 1);
    border-radius: 999px;
    width: 142px;
    height: 52px;
    padding: 16px 32px;
    border: none;
    color: rgba(255, 255, 255, 1);
    cursor: pointer;
  }
  </style>