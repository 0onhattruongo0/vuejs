<template>
  <div id="app" class="container">
      <app-header :item-count="items.length" :max-item="maxItems"></app-header>
      <app-new-items @ItemAdded="addItem" :items="items"></app-new-items>
      <app-items-layout :items="items" @itemRemove="removeItem"></app-items-layout>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Itemslayout from './components/itemslayout.vue'
import NewItems from './components/NewItems.vue'
export default {
  data: function () {
    return {
      items: [
        'I love You',
        'Hello',
        'Miss You'
      ],
      maxItems: 10
    }
  },
  components: {
    appItemsLayout: Itemslayout,
    appNewItems: NewItems,
    appHeader: Header
  },
  methods: {
    addItem (item) {
      if (this.items.length >= this.maxItems) {
        return alert('Please remove item first')
      }
      this.items.push(item)
    },
    removeItem (index) {
      this.items.splice(index, 1)
    }
  }
}
</script>

<style>

</style>
