<template>
  <div style="display: inline-block">
    <v-menu v-if="loggedIn" offset-x open-on-hover>
      <template #activator="{ on, attrs }">
        <v-avatar class="ma-1" color="grey lighten-3" :size="size" v-bind="attrs" v-on="on">
          <v-img v-if="avatar" :src="avatar" />
          <v-img v-else :src="`https://robohash.org/` + id + `.png?size=40x40`" />
        </v-avatar>
      </template>
      <v-card style="width: 200px" :to="isSelf ? '/profile' : '/profile/' + id">
        <v-card-text v-if="!$apollo.loading" class="text-center">
          <v-avatar class="my-4" color="grey lighten-3" :size="40">
            <v-img v-if="avatar" :src="avatar" />
            <v-img v-else :src="`https://robohash.org/` + id + `.png?size=40x40`" />
          </v-avatar>
          <br />
          <b>{{ user.name }}</b>
          <v-divider class="ma-4"></v-divider>
          {{ user.company }}
          <br />
          {{
            user.bio ? user.bio : 'This user prefers to keep an air of mystery around themselves.'
          }}
          <br />
        </v-card-text>
      </v-card>
    </v-menu>
    <v-avatar v-else class="ma-1" color="grey lighten-3" :size="size">
      <v-img v-if="avatar" :src="avatar" />
      <v-img v-else :src="`https://robohash.org/` + id + `.png?size=40x40`" />
    </v-avatar>
  </div>
</template>
<script>
import userQuery from '../graphql/userById.gql'
import { createClient } from '../vue-apollo'

export default {
  props: {
    avatar: String,
    name: String,
    size: {
      type: Number,
      default: 42
    },
    id: {
      type: String,
      default: null
    }
  },
  computed: {
    isSelf() {
      return this.id === localStorage.getItem('uuid')
    },
    loggedIn() {
      return localStorage.getItem('uuid') !== null
    }
  },
  apollo: {
    $client: createClient(),
    user: {
      query: userQuery,
      variables() {
        return {
          id: this.id
        }
      },
      skip() {
        return !this.loggedIn
      }
    }
  }
}
</script>
