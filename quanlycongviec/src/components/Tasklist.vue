<template>
  <table class="table table-bordered table-hover">
    <thead>
        <tr>
            <th class="text-center">STT</th>
            <th class="text-center">Tên</th>
            <th class="text-center">Trạng Thái</th>
            <th class="text-center">Hành Động</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td></td>
            <td>
                <input type="text" class="form-control" :value="searchName" @input="searchName = $event.target.value" @keyup="selectName">
            </td>
            <td>
                <select class="form-control" v-model="selectSearch" @change="select">
                    <option value='-1'>Tất Cả</option>
                    <option value="false" >Ẩn</option>
                    <option value="true">Kích Hoạt</option>
                </select>
            </td>
            <td></td>
        </tr>
         <tr v-for="(item, i) in tasks" :key="i">
            <td>{{++i}}</td>
            <td>{{item.name}}</td>
            <td class="text-center">
                <span :class="{'btn btn-success':item.status==true, 'btn btn-danger':item.status==false}" @click="updaStatus(item.id)">
                    {{item.status==true?'Kích hoạt':'Ẩn'}}
                </span>
            </td>
            <td class="text-center">
                <button type="button" class="btn btn-warning" @click="editItem(item.id)">
                    Sửa
                </button>
                &nbsp;
                <button type="button" class="btn btn-danger" @click="deleteItem(item.id)">
                    Xóa
                </button>
            </td>
        </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: ['tasks'],
  data: function () {
    return {
      selectSearch: '-1',
      searchName: ''
    }
  },
  components: {
  },
  methods: {
    deleteItem (id) {
      this.$emit('deleleItem', id)
    },
    editItem (id) {
      this.$emit('editItem', id)
    },
    updaStatus (id) {
      this.$emit('updateStatus', id)
    },
    select () {
      this.$emit('sltSearch', this.selectSearch)
    },
    selectName () {
      this.$emit('sltName', this.searchName)
    }
  }
}
</script>

<style scoped>

</style>
