<template>
<div class="row">
    <form class="">
        <div class="col-sm-8 offset-sm-2 col-md-6 offset-md-3 form-group">
          <label for="">U saying...</label>
          <textarea class="form-group" v-model="item" name="" id="" cols="30" rows="10"></textarea>
        </div>
        <div class="col-sm-8 offset-sm-2 col-md-6 offset-md-3 form-group">
          <button class="btn btn-success" @click.prevent="createNew">+Add</button>
        </div>
    </form>
</div>
</template>

<script>
export default {
  props: ['items'],
  data: function () {
    return {
      item: ''
    }
  },
  methods: {
    createNew () {
      if (this.item === '') {
        return false
      } else if (this.items.includes(this.item)) {
        return alert('This Items is exist')
      } else {
        this.$emit('ItemAdded', this.item)
        this.item = ''
      }
    }
  }
}
</script>

<style>

</style>
