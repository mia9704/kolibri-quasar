<template>
  <q-layout>
    <q-toolbar color="primary">
      <q-toolbar-title>
        <q-btn flat v-go-back=" '/' "> 
          <q-icon name="arrow_back"></q-icon> 
        </q-btn>
        Users
      </q-toolbar-title>
    </q-toolbar>
    <q-list>
      <q-item highlight v-for="user in users"@click="$router.push('/users/'+user)">
        <div class="row justify-center">
          <h5>{{user}}</h5>
        </div>
        
      </q-item>
      <!-- Inset separator example -->
      <q-item-separator inset />
    </q-list>
    <div class="row justify-center">
    <h5>Add New User</h5>
    </div>
    <div class="row justify-center">
      <q-field
        label="Username"
      >
      <q-input
        v-model="user"
        inverted color="primary"
        :after="[
          {
            icon: 'arrow_forward',
            handler () {
              add_user ()
            }
          }
        ]"
      />
    </q-field>
  </div>
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
  QItemSeparator
} from 'quasar'

export default {
  computed: {
    users () {
      return this.$store.state.users
    }
  },
  data () {
    return {
      user: ''
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
    QItemSeparator
  },
  created () {
  },
  directives: {
    GoBack
  },
  methods: {
    add_user () {
      if (this.user !== '') {
        this.$store.state.users.push(this.user)
        this.user = ''
      }
    }
  }
}
</script>

<style lang="stylus">
</style>