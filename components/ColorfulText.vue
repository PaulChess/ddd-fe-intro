<template>
  <span :style="{ color, fontWeight: bold ? 'bold' : 'normal', textDecoration: underline ? 'underline' : 'none' }">
    <slot></slot>
  </span>
</template>

<script setup>
import { defineProps } from 'vue';
defineProps({
  color: {
    type: String,
    default: 'rgb(194 70 58)',
  },
  bold: {
    type: Boolean,
    default: true,
  },
  underline: {
    type: Boolean,
    default: false,
  },
});
</script>
