<template>
  <!-- App.vue -->

  <v-app app dark>
    <v-navigation-drawer app v-model="drawer">
      <!-- -->
      <v-list subheader>
        <v-subheader>Previous chats</v-subheader>

        <v-list-tile class="users_list"
          v-for="user in users"
          :key="user.id"
        >
<!--          <v-list-item-avatar>-->
<!--            <v-img-->
<!--              :alt="`${user.name} avatar`"-->
<!--              :src="chat.avatar"-->
<!--            ></v-img>-->
<!--          </v-list-item-avatar>-->
          <v-list-tile-content>
            <v-list-tile-title>{{user.name}}</v-list-tile-title>
          </v-list-tile-content>

          <v-list-tile-action>
            <v-icon :colour="user.id===2?'primary;':'grey;'">chat_bubble</v-icon>
          </v-list-tile-action>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>

    <v-toolbar app>
      <!-- -->
      <v-toolbar-side-icon @click="drawer=!drawer"></v-toolbar-side-icon>
      <v-btn icon @click="exit">
        <v-icon>arrow_back</v-icon>
      </v-btn>
      <v-toolbar-title>Комната № {{$store.state.user.room}}</v-toolbar-title>

    </v-toolbar>

    <!-- Sizes your content based upon application components -->
    <v-content>

      <!-- Provides the application the proper gutter -->

        <!-- If using vue-router -->
        <nuxt/>
    </v-content>

  </v-app>
</template>

<script>
export default {
  data:()=>({
    drawer:true,
    users:[
      {id:1, name:'User1'},
      {id:2, name:'User2'}
    ]
  }),
  methods:{
    exit(){
      this.$router.push('/?message=leftChat')
      this.$store.commit('clearUser')
    }
  }
};
</script>

<style scoped>

</style>
