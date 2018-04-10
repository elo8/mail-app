<template>
  <div id="app">
    <!--<h1>{{ msg }}</h1>-->
    <b-container>
    <b-jumbotron header="Simple Email Application" lead="Built with vue.js" >
      <div>
      <b-form @submit="onSubmit">
      <div class="form-group">
        <label for="exampleInputEmail1">From</label>
        <input type="email" v-model="data.from" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email">
      </div>
      <div class="form-group">
        <label for="toInput">To</label>
        <input type="email" v-model="data.to" class="form-control" id="toEmail" placeholder="Enter email" multiple>
      </div>

      <div class="form-group">
        <label for="subjectInput">Subject</label>
        <input type="text" v-model="data.subject" class="form-control" id="subject" placeholder="Enter subject">
      </div>

     <div class="form-group">
      <label for="Message">Text:</label>
      <textarea class="form-control" v-model="data.text" rows="5" id="text"></textarea>
    </div>
      <!--<b-btn variant="primary" v-on:click="handleSubmit">Submit</b-btn>-->
      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button variant="danger" v-on:click="clear">Reset</b-button>
      </b-form>
      </div>
      <div class="form-group">
        <b-alert variant="success" :show="showAlert">Email request has been processed!</b-alert>
      </div>
    </b-jumbotron>
    </b-container>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: '',
      showAlert: false,
      data: {
        from: '',
        to: '',
        subject: '',
        text: ''
      }
    }
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      //alert(JSON.stringify(this.data));
      var xmlhttp = new XMLHttpRequest();   // new HttpRequest instance
      xmlhttp.open("POST", "http://localhost:8888/email");
      xmlhttp.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
      xmlhttp.send(JSON.stringify(this.data));
      //todo: handle error or check for responseBody
      //this.msg = 'Your email request has been processed';
      this.showAlert = true;
    },
    clear() {
      this.showAlert = false;
      this.data = {};
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  //margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
