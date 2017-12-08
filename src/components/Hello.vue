<template>
  <q-layout>
    <q-toolbar>
      <q-toolbar-title>
        Home
      </q-toolbar-title>
    </q-toolbar>
    <h1 >Kolibri</h1>
    <div class="row justify-center">
      <q-btn big color="primary" @click="$router.push('/users')" >users</q-btn>
    </div>
    <div class="row justify-center">
      <q-btn big color="primary" @click="$router.push('/channels')" >channels</q-btn>
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
    var usersArray = []
    axios.get('http://www.mocky.io/v2/59f0e26d310000a3270ea09a').then(function (response) {
      return response.data
    }).then(function (data) {
      for (let key in data) {
        for (let username in data[key]) {
          usersArray.push(data[key][username])
        }
      }
    })
    this.$store.state.users = usersArray
    var channels = []
    axios.get('http://127.0.0.1:8080/api/channel/').then(function (response) {
      return response.data
    }).then(function (data) {
      for (let key in data) {
        channels.push(data[key])
      }
    })
    this.$store.state.channels = channels
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
  h1,h2,h3,h4,h5 {
    text-align:center;
  }
</style>
