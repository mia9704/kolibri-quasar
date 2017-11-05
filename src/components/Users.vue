<template>
  <q-layout>
    <q-toolbar color="purple-6">
      <q-toolbar-title>
        Users
      </q-toolbar-title>
    </q-toolbar>
    <!-- <h1 class=text-purple-7>Hello!</h1>
    <div class="row justify-cen
    ter">
      <q-btn big color="purple-4" @click="$router.push('/users')" >users</q-btn>
    </div> -->
    <q-list>
      <!-- <router-link :to="{ path: '/users', params: { username: user }}"></router-link> -->
      <q-item highlight v-for="user in users"@click="$router.push('/users/'+user)"><h5 class=text-purple-4>{{user}}</h5></q-item>
      <!-- Inset separator example -->
      <q-item-separator inset />
    </q-list>
    <q-btn round big color="purple-5" v-go-back=" '/' "> 
      <q-icon name="arrow_back"></q-icon> 
    </q-btn>
  </q-layout>
</template>

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
  QItemMain,
  GoBack
} from 'quasar'
import axios from 'axios'

export default {
  data () {
    return {
      users: []
    }
  },
  props: [],
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
  },
  mounted () {
    this.listen()
  },
  created () {
    var usersArray = []
    axios.get('https://quasar-project.firebaseio.com/user.json').then(function (response) {
      // this.users = response
      // console.log(response)
      // Bus.$emit('UpdateUsers', { users: { response } })
      return response.data
    }).then(function (data) {
      console.log(data)
      for (let key in data) {
        for (let initials in data[key]) {
          for (let i in data[key][initials]) {
            // usersArray.push(data[key][initials[i]])
            console.log(data[key][initials][i])
            usersArray.push(data[key][initials][i])
          }
        }
      }
    })
    this.users = usersArray
  },
  directives: {
    GoBack
  },
  methods: {
    listen () {
      // Bus.$on('UpdateUsersData', (event) => {
      //   console.log(event.users)
      // })
    }
  }
}
</script>

<style lang="stylus">
</style>