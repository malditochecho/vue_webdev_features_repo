<script setup lang="ts">
// IMPORTS
import { onMounted, ref } from 'vue'

// TYPES
interface Item {
  id: number
  url: string
}

// DATA
const source = [
  { id: 10, url: `https://picsum.photos/id/10/400/400` },
  { id: 11, url: `https://picsum.photos/id/11/400/400` },
  { id: 12, url: `https://picsum.photos/id/12/400/400` },
  { id: 13, url: `https://picsum.photos/id/13/400/400` },
  { id: 14, url: `https://picsum.photos/id/14/400/400` },
  { id: 15, url: `https://picsum.photos/id/15/400/400` },
  { id: 16, url: `https://picsum.photos/id/16/400/400` },
  { id: 17, url: `https://picsum.photos/id/17/400/400` },
  { id: 18, url: `https://picsum.photos/id/18/400/400` },
  { id: 19, url: `https://picsum.photos/id/19/400/400` },
  { id: 20, url: `https://picsum.photos/id/20/400/400` },
  { id: 21, url: `https://picsum.photos/id/21/400/400` },
  { id: 22, url: `https://picsum.photos/id/22/400/400` },
  { id: 23, url: `https://picsum.photos/id/23/400/400` },
  { id: 24, url: `https://picsum.photos/id/24/400/400` },
  { id: 25, url: `https://picsum.photos/id/25/400/400` },
  { id: 26, url: `https://picsum.photos/id/26/400/400` },
  { id: 27, url: `https://picsum.photos/id/27/400/400` },
  { id: 28, url: `https://picsum.photos/id/28/400/400` },
  { id: 29, url: `https://picsum.photos/id/29/400/400` },
  { id: 30, url: `https://picsum.photos/id/30/400/400` }
]

// REACTIVE DATA
const items = ref<Item[]>([])
const selectedItems = ref<Item[]>([])

// METHODS

/**
 * Check if the item is already added to the selectedItems array
 * @param id - The item id to check
 * @returns boolean
 */
const checkItemAlreadyAdded = (id: number): boolean => {
  return selectedItems.value.some((item) => item.id === id)
}

/**
 * Shuffle the items array and get 10 random items
 */
const shuffleItems = (): void => {
  items.value = source.sort(() => 0.5 - Math.random()).slice(0, 20)
}

/**
 * Fake insert the selected items to a DB
 */
const saveItems = (): void => {
  alert(`Saved ${selectedItems.value.length} items to the DB`)
}

/**
 * Add or remove the item from the selectedItems array
 * @param item - The item to add or remove
 */
const toggleItem = (item: Item): void => {
  const index = selectedItems.value.findIndex((img) => img.id === item.id)
  if (index === -1) selectedItems.value.push(item)
  else selectedItems.value.splice(index, 1)
}

// LIFE CYCLE
onMounted(() => {
  shuffleItems()
})
</script>

<template>
  <main
    class="relative flex min-h-svh min-w-full justify-center bg-gradient-to-r from-emerald-500 to-emerald-900 p-4"
    :class="[selectedItems.length > 0 ? 'px-4 py-4 pb-44' : 'p-4']"
  >
    <div class="flex max-w-lg flex-col items-center justify-center space-y-4">
      <!-- get items button -->
      <button
        class="w-full border border-purple-700 bg-violet-500 p-2 text-white shadow-xl hover:bg-violet-600 focus:outline-none focus:ring focus:ring-violet-300 active:bg-violet-700"
        @click.stop="shuffleItems"
      >
        Fetch new items
      </button>

      <!-- items -->
      <p class="font-medium text-white">ℹ️ Add items by clicking on them</p>
      <div class="grid grid-cols-2 gap-3">
        <div v-for="item in items" :key="item.id">
          <button @click.stop="toggleItem(item)">
            <img
              :src="item.url"
              loading="lazy"
              class="border-8 border-gray-300"
              :class="[checkItemAlreadyAdded(item.id) ? 'brightness-50' : '']"
            />
          </button>
        </div>
      </div>
    </div>

    <!-- selected items -->
    <div v-if="selectedItems.length > 0" class="fixed bottom-0 h-40 w-full space-y-4 bg-black p-4">
      <div class="mx-auto flex max-w-lg space-x-2 overflow-x-scroll">
        <img
          v-for="item in selectedItems"
          :key="item.id"
          :src="item.url"
          class="h-16 w-16"
          @click.stop="toggleItem(item)"
        />
      </div>
      <button
        class="h-12 w-full bg-violet-500 p-2 text-white hover:bg-violet-600 focus:outline-none focus:ring focus:ring-violet-300 active:bg-violet-700"
        @click.stop="saveItems"
      >
        Save items
      </button>
    </div>
  </main>
</template>
