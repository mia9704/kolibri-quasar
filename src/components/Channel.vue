<template>
  <q-layout>
    <q-toolbar>
      <q-toolbar-title>
        <q-btn flat @click=" $router.go(-1) "> 
          <q-icon name="arrow_back"></q-icon> 
        </q-btn>
        Channel
      </q-toolbar-title>
    </q-toolbar>
    <h3>
      {{ channel['name'] }}
      <router-view :key></router-view>
    </h3>
    <div class="row justify-center">
      <h5 class=text-primary>
        {{ channel['description'] }}
        <router-view :key></router-view>
      </h5>
    </div>
    <q-list>
      <router-view :key></router-view>
      <q-item highlight v-for="node in contentNode"@click="$router.push('/channels/'+node['pk'])">
        <q-card inline style="width: 500px">
          <q-card-media>
            <q-parallax :src="'statics/folder.png'":height="150">
            </q-parallax>
            <q-card-separator />
            <q-card-title>
              <h5>{{node['title']}}</h5>
            </q-card-title>
          </q-card-media>
        </q-card>
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
  QItemSeparator,
  QCard,
  QCardTitle,
  QCardMain,
  QCardSeparator,
  QCardMedia,
  QParallax,
  GoBack
} from 'quasar'
import axios from 'axios'
export default {
  computed: {
    key () {
      return this.$route.params.root
    }
  },
  data () {
    return {
      channel: {},
      channelKey: '',
      contentNode: {}
      // key: this.$route.params.root
      // key: '',
    }
  },
  watch: {
    key (newVal) {
      this.updateContents(newVal)
    }
  },
  mounted () {
    this.updateContents()
  },
  methods: {
    updateContents (key) {
      var key2 = key || this.$route.params.root
      var contentNode = []
      for (let key in this.$store.state.channels) {
        let channel = this.$store.state.channels[key]
        if (channel['root'] === key2) {
          this.channel = channel
          this.channelKey = key
        }
      }
      axios.get('http://127.0.0.1:8080/api/contentnode/?parent=' + this.key).then(function (response) {
        return response.data
      }).then(function (data) {
        for (let key in data) {
          contentNode.push(data[key])
        }
      })
      this.$store.state.channels[this.channelKey]['contentNode'] = contentNode
      this.contentNode = contentNode
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
    QItemSeparator,
    QCard,
    QCardTitle,
    QCardMain,
    QCardSeparator,
    QCardMedia,
    QParallax,
    QItemMain
  },
  directives: {
    GoBack
  }
}
</script>