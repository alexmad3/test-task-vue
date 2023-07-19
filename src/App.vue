<script setup>
  import { ref } from 'vue';
  import { userItems, items } from './constants';
  import ItemCard from './components/ItemCard.vue';

  const selectedUserItems = ref([]);
  const selectedItem = ref({});

  function selectItems (item) {
    const findedIndexItem = selectedUserItems.value.findIndex(el => el.id === item.id);

    if (findedIndexItem >= 0) {
      selectedUserItems.value.splice(findedIndexItem, 1);
      item.isSelected = false;
    } else if (findedIndexItem === -1 && selectedUserItems.value.length < 6) {
      selectedUserItems.value.push(item);
      item.isSelected = true;
    } else {
      alert('The maximum number of items for the user is selected');
    }
  }

  function selectItem (item) {
    selectedItem.value = item.id === selectedItem.value.id ? {} : item;
  }
</script>

<template>
  <div class="app__container app_full-height">
    <div class="app__section">
      <div class="app__selected-items">
        <div class="app__items">
          <item-card
            v-for="item in selectedUserItems"
            :key="item.id"
            :name="item.name"
            @click="selectItems(item)"
          />
        </div>

        selected: {{ selectedUserItems.length }} / 6 
      </div>

      <div
        class="app__selected-item"
        :class="{ 'app__selected-item_selected': !!selectedItem.name }"
        @click="!!selectedItem.name ? selectItem(selectedItem) : null"
      >
        {{ selectedItem.name || 'Item not selected' }}
      </div>
    </div>

    <div class="app__section app_full-height">
      <div class="app__container_items app__items">
        <item-card
          v-for="item in userItems"
          :key="item.id"
          :name="item.name"
          :isSelected="item.isSelected"
          @click="selectItems(item)"
        />
      </div>

      <div class="app__container_items app__items">
        <item-card
          v-for="item in items"
          :key="item.id"
          :name="item.name"
          :isSelected="item.id === selectedItem.id"
          @click="selectItem(item)"
        />
      </div>
    </div>
  </div>
</template>

<style>
  .app__container {
    display: flex;
    flex-direction: column;
    row-gap: 2rem;
  }

  .app__section {
    display: flex;
    justify-content: space-between;
  }

  .app__selected-items,
  .app__selected-item {
    width: 300px;
    min-height: 200px;
    border: var(--border-base);
  }

  .app__selected-items {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 1rem;
  }

  .app__selected-item {
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    transition: var(--transition);
  }

  .app__selected-item_selected:hover {
    box-shadow: inset 0 0 1rem var(--primary);
    border-color: var(--primary);
    cursor: pointer;
  }

  .app__items {
    display: flex;
    flex-wrap: wrap;
    align-content: flex-start;
    gap: 1rem;
  }

  .app__container_items {
    width: calc(50vw - 5rem);
    border: var(--border-base);
    padding: 1rem;
  }

  .app_full-height {
    height: 100%;
  }
</style>
