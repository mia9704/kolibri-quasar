<template>
  <q-layout>
    <q-toolbar color="primary">
      <q-toolbar-title>
        User
      </q-toolbar-title>
    </q-toolbar>
    <h1 class=text-primary>
      {{ $route.params.username }}
    </h1>
    <q-btn round big color="primary" v-go-back=" '/users' "> 
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
  directives: {
    GoBack
  },
  created () {
    var usersArray = []
    axios.get('https://quasar-project.firebaseio.com/user.json').then(function (response) {
      return response.data
    }).then(function (data) {
      for (let key in data) {
        for (let initials in data[key]) {
          for (let i in data[key][initials]) {
            usersArray.push(data[key][initials][i])
          }
        }
      }
    })
    this.users = usersArray
  }
}
</script>

<style lang="stylus">
</style>