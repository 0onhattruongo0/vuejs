<template>
  <div id="app" class="container">
    <h1 class="text-center">Quản lý công việc</h1>
    <hr>
    <div class="row">
      <div class="col-4" v-if="addForm">
        <app-form @removeForm="rmForm" @save='addItem' @update='updateItem' :id="id" :data="data"></app-form>
      </div>
      <div :class="{'col-8':addForm, 'col-12':!addForm}">
         <button type="button" class="btn btn-primary outline" @click="addForm=!addForm, id =''">
            Thêm Công Việc
        </button>
        <div class="row mt-3">
            <div class="col-12">
               <app-task-list @sltSearch="sltSearch" @sltName="sltName" :searchName="searchName" :tasks="filterSearch" @deleleItem="dltItem" :selectSearch="selectSearch" @editItem="editItem" @updateStatus="updateStatus"></app-task-list>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Form from './components/Form.vue'
import TaskList from './components/Tasklist.vue'
export default {
  data: function () {
    return {
      addForm: false,
      id: '',
      tasks: [{
        id: 1,
        name: 'Test1',
        status: true
      }, {
        id: 2,
        name: 'Test2',
        status: false
      }, {
        id: 3,
        name: 'Test3',
        status: true
      }],
      data: {
        name: '',
        status: 'true'
      },
      selectSearch: '-1',
      searchName: ''
    }
  },
  components: {
    appForm: Form,
    appTaskList: TaskList
  },
  computed: {
    filterSearch: function () {
      if (this.searchName === '') {
        return this.tasks.filter((tasks) => {
          if (this.selectSearch === '-1') {
            return tasks
          } if (this.selectSearch === true) {
            return tasks.status === true
          } else {
            return tasks.status === false
          }
        })
      } else {
        return this.tasks.filter((tasks) => {
          if (this.selectSearch === '-1') {
            return tasks.name.toLowerCase().indexOf(this.searchName.toLowerCase()) !== -1
          } if (this.selectSearch === true) {
            return tasks.status === true & tasks.name.toLowerCase().indexOf(this.searchName.toLowerCase()) !== -1
          } else {
            return tasks.status === false & tasks.name.toLowerCase().indexOf(this.searchName.toLowerCase()) !== -1
          }
        })
      }
    }
  },
  methods: {
    rmForm () {
      this.addForm = !this.addForm
    },
    addItem (item) {
      if (item.status === 'true') {
        item.status = true
      } else {
        item.status = false
      }
      this.tasks.push(item)
      this.addForm = false
    },
    dltItem (id) {
      this.tasks.splice(this.tasks.findIndex(a => a.id === id), 1)
      this.addForm = false
    },
    editItem (id) {
      this.id = id
      this.addForm = true
      this.dataEdit1 = (this.tasks[this.tasks.findIndex(a => a.id === id)])
      this.data.name = this.dataEdit1.name
      this.data.status = this.dataEdit1.status
    },
    updateItem (item) {
      this.dataUpdate = this.tasks[this.tasks.findIndex(a => a.id === item[1])]
      console.log(this.dataUpdate)
      if (item[0].status === 'true' | item[0].status === true) {
        item[0].status = true
      } else {
        item[0].status = false
      }
      this.dataUpdate.name = item[0].name
      this.dataUpdate.status = item[0].status
      this.addForm = false
      this.data.name = ''
      this.data.status = 'true'
      this.id = ''
    },
    updateStatus (id) {
      this.dataUpdate = this.tasks[this.tasks.findIndex(a => a.id === id)]
      console.log(this.dataUpdate)
      this.dataUpdate.status = !this.dataUpdate.status
    },
    sltSearch (select) {
      this.tasks = this.tasks
      if (select === '-1') {
        this.selectSearch = '-1'
      }
      if (select === 'true') {
        this.selectSearch = true
      }
      if (select === 'false') {
        this.selectSearch = false
      }
    },
    sltName (name) {
      this.searchName = name
    }
  }
}
</script>

<style>

</style>
