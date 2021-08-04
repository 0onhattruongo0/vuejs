<template>
  <div id="app" class="container">
    <form>
      <div class="row">
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
          <h1 class="text-center">Form section</h1>
          <hr>
          <div class="form-group">
            <label for="">Mail</label>
            <!-- <input type="text" id="email" class="form-control" v-model.lazy="useData.email"> -->
            <input type="text" id="email" class="form-control" :value="useData.email" @input="useData.email = $event.target.value">
          </div>
          <div class="form-group">
            <label for="">Password:</label>
            <input type="password" id="password" class="form-control" v-model="useData.password">
          </div>
          <div class="form-group">
            <label for="">Age</label>
            <input type="text" id="age" class="form-control" v-model="useData.age">
          </div>
          <div class="form-group">
            <label for="">Message</label>
            <textarea name="message" id="" cols="30"  rows="5" class="form-control" v-model="useData.message"></textarea>
          </div>
          <div class="form-group">
              <label for="sendMail">
                <input type="checkbox" id="sendmail" value="sendmail" v-model="useData.sendEmail">SendMail
              </label>
              <label for="sendInfoMail">
                <input type="checkbox" id="sendinfomail" value="sendinfomail" v-model="useData.sendEmail">SendInfoMail
              </label>
              <label for="cutMail">
                <input type="checkbox" id="cutMail" value="cutMail" v-model="useData.sendEmail">Cut Mail
              </label>
            </div>
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
            <div class="form-check">
              <input class="form-check-input" type="radio" name="Male" id="Male" value="Male" v-model="useData.Gender">
              <label class="form-check-label" for="Male">
                Male
              </label>
            </div>
            <div class="form-check">
              <input class="form-check-input" type="radio" name="Female" id="Female" value="Female" v-model="useData.Gender">
              <label class="form-check-label" for="exampleRadios2">
                Female
              </label>
            </div>
          </div>
          <div class="form-group">
              <label for="">Priorities:</label>
              <select class="form-control" name="priority" id="priorities" v-model="selectedPriority">
                <option v-for="item in useData.priorities" v-bind:key="item">{{item}}</option>
              </select>
          </div>
          <div class="form-group">
              <label for="">Switched:</label>
                <app-custom v-model="useData.dataswitch"></app-custom>
          </div>
          <div>
            <button class="btn btn-primary" @click.prevent="submited">Submit</button>
          </div>
        </div>
      </div>
    </form>
    <hr>
    <div class="row" v-if="isSubmit">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset3">
        <div class="card">
          <div class="card-header">
            <h4>Your Data</h4>
          </div>
          <div class="card-body">
            <p>Mail:{{useData.email}}</p>
            <p>Password:{{useData.password}}</p>
            <p>Age: {{useData.age}}</p>
            <p style="white-space: pre">Message:{{useData.message}}</p>
            <p><strong>SendMail</strong></p>
            <ul>
              <li v-for="item in useData.sendEmail" v-bind:key="item" >{{item}}</li>
            </ul>
            <p>Gender:{{useData.Gender}}</p>
            <p>Priority:{{selectedPriority}}</p>
            <p>Switched: {{useData.dataswitch}}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Custom from './components/customcontrol.vue'
export default {
  data: function () {
    return {
      useData: {
        email: '',
        password: '',
        age: '',
        message: '',
        sendEmail: [],
        Gender: 'Male',
        priorities: ['High', 'Medium', 'Low'],
        dataswitch: true
      },
      selectedPriority: 'Low',
      isSubmit: false
    }
  },
  methods: {
    submited () {
      this.isSubmit = true
    }
  },
  components: {
    appCustom: Custom
  }
}
</script>

<style>

</style>
