<template>
  <!-- App.vue -->

  <v-app app dark>
    <v-navigation-drawer app v-model="drawer" mobile-break-point="650">
      <!-- -->
      <v-list subheader>
        <v-subheader>Список пользователей</v-subheader>

        <v-list-tile class="users_list"
                      v-for="user in $store.state.users"
                      :key="user.id"
                     @click="showDescription(user)"
                     title="Подробнее"
        >
<!--          <v-list-item-avatar>-->
<!--            <v-img-->
<!--              :alt="`${user.name} avatar`"-->
<!--              :src="chat.avatar"-->
<!--            ></v-img>-->
<!--          </v-list-item-avatar>-->
          <v-list-tile-content >
            <div class="avatar">
              <v-avatar :color="user.id===$store.state.user.id?'primary':'grey'" size="30">
                <span class="white--text text-h7">{{user.name[0].toUpperCase()}}</span>
              </v-avatar>
            </div>
          </v-list-tile-content>
          <v-list-tile-content class="item-user">
            <v-list-tile-title class="user-title">{{user.name}}</v-list-tile-title>
          </v-list-tile-content>
          <v-list-tile-action @click.stop="$router.push('/chat')">
            <v-icon class="icon" :color="user.id===$store.state.user.id?'primary':'grey'">chat_bubble</v-icon>
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
        <div style="height: 100%">
        <!-- If using vue-router -->
           <nuxt/>
        </div>
    </v-content>

  </v-app>
</template>

<script>
export default {
  data:()=>({
    drawer:true,
  }),
  methods:{
    exit(){
        this.$socket.emit('userLeft',this.$store.state.user.id,()=>{
        this.$router.push('/?message=leftChat')
        this.$store.commit('clearUser')
      })

    },
    showDescription(user){
      // this.$router.push('/aboutUser', user)
      // console.log(user)
      this.$router.push({path:`/chat/${user.name}`, query:{name:user.name}})
    }
  }
};
</script>

<style scoped>
.avatar{
  margin-left: 10px;
  cursor: pointer;
  transition: all .2s ease-in-out;
  border-radius: 200px;
  border: none;
}


.icon{
  cursor: pointer;
  color: white;
}
.icon:hover{
  transform: scale(1.6);
}
.users_list{
  cursor: pointer;

  margin-bottom: 10px;
}
.users_list:hover{
  background-color: darkslateblue;
  border-radius: 2px;
}
.user-title{
  font-size: 20px;
}
.users_list:hover  .user-title{
  font-size: 21px;
  letter-spacing: 2px;
}
.users_list:hover .avatar{
  transform: scale(1.2);
  box-shadow: 0px 4px deepskyblue;
}

</style>
