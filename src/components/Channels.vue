<template>
  <q-layout>
    <q-toolbar>
      <q-toolbar-title>
        <q-btn flat v-go-back=" '/' "> 
          <q-icon name="arrow_back"></q-icon> 
        </q-btn>
        Channels
      </q-toolbar-title>
    </q-toolbar>
    <q-list>
      <q-item highlight v-for="channel in channels"@click="$router.push('/channels/'+channel['root'])">
        <q-card-media>
          <q-parallax :src="channel['thumbnail']":height="150">
          </q-parallax>
          <q-card-separator />
          <q-card-title>
            <h5>{{channel['name']}}</h5>
          </q-card-title>
        </q-card-media>
      </q-item>
      <q-item-separator inset />
    </q-list>
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
  GoBack,
  QInput,
  QField,
  QItemSeparator,
  QCard,
  QCardTitle,
  QCardMain,
  QCardSeparator,
  QCardMedia,
  QParallax
} from 'quasar'
export default {
  computed: {
    channels () {
      return this.$store.state.channels
    }
  },
  data () {
    return {
      channel: ''
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
    QItemMain,
    QInput,
    QField,
    QItemSeparator,
    QCard,
    QCardTitle,
    QCardMain,
    QCardSeparator,
    QCardMedia,
    QParallax
  },
  created () {
  },
  directives: {
    GoBack
  }
}
</script>

<style lang="stylus">
</style>