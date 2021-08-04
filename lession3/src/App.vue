<template>
  <div id="app">
    <div class="row">
      <div>
        <button class="btn btn-outline-danger" @click="selectedComponent='appCard'">AppCard</button>
        <button class="btn btn-outline-danger" @click="selectedComponent='appContact'">Contact</button>
        <button class="btn btn-outline-danger" @click="selectedComponent='appAbout'">About</button>
      </div>
    </div>
    <p>{{selectedComponent}}</p>
    <div class="container">
      <!-- <app-card cardWords="Cat">
        <h1>Test1</h1>
        <h1>Test2</h1>
      </app-card> -->
      <component :is="selectedComponent"></component>
    </div>
  </div>
</template>

<script>
import Card from './components/Card.vue'
import About from './components/About.vue'
import Contact from './components/Contact.vue'
export default {
  data: function () {
    return {
      selectedComponent: 'appCard'
    }
  },
  components: {
    appCard: Card,
    appAbout: About,
    appContact: Contact
  }
}
</script>

<style>

</style>
