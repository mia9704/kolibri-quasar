<template>
  <q-layout>
    <q-toolbar color="purple-6">
      <q-toolbar-title>
        Home
      </q-toolbar-title>
    </q-toolbar>
    <!--<h1 class=text-purple-7>Users</h1>
    <q-btn round big color="purple-4" @click="$router.push('/time')"> 
      <q-icon name="access_time"></q-icon> 
    </q-btn>-->
    <h1 class=text-purple-7>Hello!</h1>
    <div class="row justify-center">
      <q-btn big color="purple-4" @click="$router.push('/users')" >users</q-btn>
    </div>
  </q-layout>
</template>
<script src="https://www.gstatic.com/firebasejs/4.6.0/firebase-database.js"></script>
<script src="https://www.gstatic.com/firebasejs/4.6.0/firebase.js"></script>
<script>
  import Vue from 'vue'
  import VueFire from 'vuefire'
  Vue.use(VueFire)
  var firebase = require('firebase/app')
  require('firebase/auth')
  require('firebase/database')
  // Initialize Firebase
  var config = {
    apiKey: 'AIzaSyA2rAhDlQqlhwGbzvRWtMUKhMTIUcA7rEw',
    authDomain: 'quasar-project.firebaseapp.com',
    databaseURL: 'https://quasar-project.firebaseio.com',
    projectId: 'quasar-project',
    storageBucket: 'quasar-project.appspot.com',
    messagingSenderId: '552768185338'
  }
  firebase.initializeApp(config)
</script>
<script>
import {
  QLayout,
  QToolbar,
  QToolbarTitle,
  QBtn,
  QIcon,
  QList,
  QListHeader,
  QItem,
  QItemSide,
  QItemMain
} from 'quasar'
import axios from 'axios'
export default {
  data () {
    return {
      users: [],
      hi: 'Mia'
    }
  },
  mounted () {
    // axios.post('https://quasar-project.firebaseio.com/user.json', this.users).then(function (response) {
    //   this.users = response
    //   console.log(response)
    // }).catch(function (error) {
    //   console.log(error)
    // })
    var usersArray = []
    axios.get('http://www.mocky.io/v2/59f0e26d310000a3270ea09a').then(function (response) {
      return response.data
    }).then(function (data) {
      console.log(data)
      for (let key in data) {
        for (let username in data[key]) {
          console.log(data[key][username])
          usersArray.push(data[key][username])
        }
      }
    })
    this.$store.state.users = usersArray
  },
  name: 'index',
  components: {
    QLayout,
    QToolbar,
    QToolbarTitle,
    QBtn,
    QIcon,
    QList,
    QListHeader,
    QItem,
    QItemSide,
    QItemMain
  }
}
</script>

<style lang="stylus">
  h1 {
    text-align:center;
  }
</style>
