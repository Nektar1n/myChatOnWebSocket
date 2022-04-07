<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8>
      <v-card min-width="400">
            <v-snackbar
              v-model="snackbar"
              :timeout="6000"
              top
            >
              {{ message }}
                <v-btn
                  color="blue"
                  flat
                  @click="snackbar = false"
                >
                  Закрыть
                </v-btn>
            </v-snackbar>
          <v-card-title><h1>conf_Room</h1></v-card-title>
          <v-card-text>
          <v-form
            class="open_form"
            ref="form"
            v-model="valid"
            lazy-validation
          >
            <v-text-field
              v-model="name"
              :counter="16"
              :rules="nameRules"
              label="Твоё имя"
              required
            ></v-text-field>

            <v-text-field
              v-model="room"
              :rules="roomRules"
              label="Введи id комнаты"
              required
            ></v-text-field>

<!--            <v-checkbox-->
<!--              v-model="checkbox"-->
<!--              :rules="[v => !!v || 'You must agree to continue!']"-->
<!--              label="Do you agree?"-->
<!--              required-->
<!--            ></v-checkbox>-->

            <v-btn
              :disabled="!valid"
              color="success"
              class="mr-4"
              @click="submit"
            >
              Войти
            </v-btn>

            <v-btn
              color="error"
              class="mr-4"
              @click="reset"
            >
              Очистить
            </v-btn>

          </v-form>
          </v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</template>


<script>




export default {
  layout:'empty',
  head:{
    title: 'Добро пожаловать в conf_Room'
  },
  sockets: {
    connect: function() {
      console.log("socket connected");
    }
  },
  data: () => ({
    valid: true,
    name: '',
    nameRules: [
      v => !!v || 'Имя не может быть пустым',
      v => (v && v.length <= 16) || 'Имён больше 16 букв не существует',
    ],
    room: '',
    roomRules: [
      v => !!v || 'Пустая комната',
      // v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    snackbar:false,
    message:'',

  }),

  methods: {
    submit () {
      if(this.$refs.form.validate()){
          const user={
            name: this.name,
            room: this.room
          }

          this.$socket.emit('userConnected', user, data=>{
              if (typeof data==='string'){
                console.error(data)
              }else {
                user.id=data.userId
                this.$store.commit('setUser',user)
                this.$router.push('/chat')

              }
          });

      }
    },
    reset () {
      this.$refs.form.reset()
    },
  },
  mounted() {
    const {message}=this.$route.query
    if (message==='noUser'){
      this.message='Введите данные'
    }else if (message==='leftChat'){
      this.message='Вы вышли из чата'
    }

    this.snackbar=!!this.message
  }
}
</script>

<style>
h1{
  margin: 0 auto;
}

</style>
