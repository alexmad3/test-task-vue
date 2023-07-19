<script setup>
defineProps({
  name: String,
  isSelected: Boolean,
})
</script>

<template>
  <div
    class="item-card"
    :class="{'item-card_selected': isSelected}"
  >
    <span>{{ name }}</span>
  </div>
</template>

<style>
  .item-card {
    padding: 1rem 2rem;
    border: var(--border-base);
    cursor: pointer;
    user-select: none;
    transition: var(--transition);
  }

  .item-card:hover {
    box-shadow: inset 0 0 1rem var(--primary);
    border-color: var(--primary);
  }

  .item-card_selected {
    box-shadow: inset 0 0 1rem var(--warning);
    border-color: var(--warning);
  }
</style>
