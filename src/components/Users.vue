<template>
  <q-layout>
    <q-toolbar color="purple-6">
      <q-toolbar-title>
        <q-btn flat v-go-back=" '/' "> 
          <q-icon name="arrow_back"></q-icon> 
        </q-btn>
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
      <q-item highlight v-for="user in users"@click="$router.push('/users/'+user)">
        <div class="row justify-center">
          <h5 class=text-purple-5>{{user}}</h5>
        </div>
        
      </q-item>
      <!-- Inset separator example -->
      <q-item-separator inset />
    </q-list>
    <div class="row justify-center">
    <h5 class=text-purple-7>Add New User</h5>
    </div>
    <div class="row justify-center">
      <q-field
        label="Username"
      >
      <q-input
        v-model="user"
        inverted color="purple-4"
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
  mounted () {
    this.listen()
  },
  created () {
    /* var usersArray = []
    axios.get('http://www.mocky.io/v2/59f0e26d310000a3270ea09a').then(function (response) {
      // this.users = response
      // console.log(response)
      // Bus.$emit('UpdateUsers', { users: { response } })
      return response.data
    }).then(function (data) {
      console.log(data)
      for (let key in data) {
        for (let username in data[key]) {
          // usersArray.push(data[key][initials[i]])
          console.log(data[key][username])
          usersArray.push(data[key][username])
        }
      }
    })
    this.users = usersArray*/
  },
  directives: {
    GoBack
  },
  methods: {
    listen () {
      // Bus.$on('UpdateUsersData', (event) => {
      //   console.log(event.users)
      // })
    },
    add_user () {
      this.$store.state.users.push(this.user)
      this.user = ''
    }
  }
}
</script>

<style lang="stylus">
</style>