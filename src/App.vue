<template>
  <div class="header-items">
    <div class="header-items__left header-left">
      <div
        v-if="leftSelectedItems.length"
        v-for="(item, index) in leftSelectedItems"
        :key="index"
        class="header-left__item item"
      >
        {{ item.name }}
      </div>

      <div class="header-left__selected-text">
        selected: {{ leftItemsSelectedCount }} / {{ totalLeftCount }}
      </div>
    </div>

    <div class="header-items__right header-right">
      <div v-if="rightSelectedItem !== undefined" class="header-right__item item">
        {{ rightItems[rightSelectedItem].name }}
      </div>

      <div v-else class="header-right__selected-text">Selected item</div>
    </div>
  </div>

  <div class="body-items">
    <div class="body-items__left body-left">
      <div
        v-for="(item, index) in leftItems"
        :key="index"
        class="body-left__item item"
        @click="selectLeftItem(index)"
      >
        {{ item.name }}
      </div>
    </div>

    <div class="body-items__right body-right">
      <div
        v-for="(item, index) in rightItems"
        class="body-right__item item"
        @click="selectRightItem(index)"
      >
        {{ item.name }}
      </div>
    </div>
  </div>

  <button @click="resetLeftItems" :disabled="leftItemsSelectedCount === 0">Reset left items</button>

  <button @click="resetRightItems" :disabled="rightSelectedItem === undefined">
    Reset right items
  </button>
</template>

<script setup lang="ts">
// Vue
import { ref } from 'vue';

const leftItemsSelectedCount = ref(0);
const totalLeftCount = 6;

const leftSelectedItems = ref<Item[]>([]);
const rightSelectedItem = ref<number>();

/**
 * @description Item
 * @type {Item}
 */
interface Item {
  id: number;
  name: string;
}

/**
 * @description Left items collection
 * @type {Item[]}
 */
const leftItems: Item[] = [
  {
    id: 1,
    name: 'Shoes 1',
  },
  {
    id: 2,
    name: 'Shoes 2',
  },
  {
    id: 3,
    name: 'Shoes 3',
  },
  {
    id: 4,
    name: 'Shoes 4',
  },
  {
    id: 5,
    name: 'T-shirt 1',
  },
  {
    id: 6,
    name: 'T-shirt 2',
  },
  {
    id: 7,
    name: 'T-shirt 3',
  },
  {
    id: 8,
    name: 'T-shirt 4',
  },
];

/**
 * @description Right items collection
 * @type {Item[]}
 */
const rightItems: Item[] = [
  {
    id: 11,
    name: 'Jacket 1',
  },
  {
    id: 12,
    name: 'Jacket 2',
  },
  {
    id: 13,
    name: 'Jacket 3',
  },
  {
    id: 14,
    name: 'Jacket 4',
  },
  {
    id: 15,
    name: 'Hoodie 1',
  },
  {
    id: 16,
    name: 'Hoodie 2',
  },
  {
    id: 17,
    name: 'Hoodie 3',
  },
  {
    id: 18,
    name: 'Hoodie 4',
  },
];

/**
 * @description Select left item
 * @param index
 */
const selectLeftItem = (index: number) => {
  if (
    leftSelectedItems.value.includes(leftItems[index]) ||
    leftSelectedItems.value.length === totalLeftCount
  )
    return;
  leftSelectedItems.value.push(leftItems[index]);
  leftItemsSelectedCount.value = leftSelectedItems.value.length;
};

/**
 * @description Select right item
 * @param index
 */
const selectRightItem = (index: number) => {
  rightSelectedItem.value = index;
};

const resetLeftItems = () => {
  leftSelectedItems.value = [];
  leftItemsSelectedCount.value = 0;
};

const resetRightItems = () => {
  rightSelectedItem.value = undefined;
};
</script>

<style lang="scss">
.header-items {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  padding: 2rem;
  border: 2px solid var(--border-color);
}

.header-left {
  // .header-left__selected-text
  &__selected-text {
    grid-column: 1 / -1;
  }
}

.item {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100px;
  height: 100px;
  cursor: pointer;
  border: 1px solid var(--border-color);
}

.header-right,
.header-left {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  gap: 1rem;
  max-width: 50%;
  padding: 1rem;
  overflow: hidden;
  border: 2px solid var(--border-color);

  .item {
    cursor: default;
  }
}

.body-left,
.body-right {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  gap: 1rem;
  max-width: 50%;
  padding: 1rem;
  overflow: hidden;
  border: 2px solid var(--border-color);
}

.body-items {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  padding: 2rem;
  margin-top: 2rem;
  border: 2px solid var(--border-color);
}
</style>
