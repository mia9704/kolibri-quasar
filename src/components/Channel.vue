<template>
  <q-layout>
    <q-toolbar>
      <q-toolbar-title>
        Channel
      </q-toolbar-title>
    </q-toolbar>
    <h1 class=text-primary>
      {{ channel['name'] }}
    </h1>
    <div class="row justify-center">
      <h5 class=text-primary>
        {{ channel['description'] }}
      </h5>
    </div>
    <q-btn round big color="primary" v-go-back=" '/channels' "> 
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
  computed: {
    channel () {
      for (let key in this.$store.state.channels) {
        let channel = this.$store.state.channels[key]
        if (channel['root'] === this.$route.params.root) {
          return channel
        }
      }
    }
  },
  data () {
    return {
      channels: []
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
  }
}
</script>

<style lang="stylus">
</style>