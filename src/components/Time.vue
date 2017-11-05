<template>
  <q-layout>
    <q-toolbar color="purple-6">
      <q-toolbar-title>
        Time Now
      </q-toolbar-title>
    </q-toolbar>
    <h1 class=text-purple-7> The time is ...</h1>
    <h6 class=text-purple-4>{{currTime()}}</h6>
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

export default {
  name: 'time',
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
    QItemMain,
    GoBack
  },
  data: function () {
    return {
      time: '???'
    }
  },
  directives: {
    GoBack
  },
  methods: {
    currTime: function (e) {
      var dateFormat = require('dateformat')
      var now = new Date()
      this.time = dateFormat(now, 'dddd, mmmm dS, yyyy, h:MM:ss TT')
      return this.time
    }
  }
}
</script>

<style lang="stylus">
  h1 {
    text-align:center;
  }
  h6 {
    text-align:center;
  }
</style>
