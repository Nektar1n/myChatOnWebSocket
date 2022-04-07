<template>
  <div class="container">
        <v-flex xs12>
          <v-text-field
            class="text-field"
            v-model="message"
            @keydown.enter="send"
            label="Введите сообщение"
            clearable
            color="white"
          ></v-text-field>
        </v-flex>
        <v-btn light class="btn" @click="send">Отправить</v-btn>
  </div>
</template>

<script>
export default {
  name:"ChatForm",
  data: () => ({
    message: '',
  }),
  methods: {
    send(){
      this.$emit('scrollBottom')
      this.$socket.emit('createMessage',{
        text: this.message,
        id: this.$store.state.user.id
      }, (data)=>{
        if (typeof data==='string'){
          console.error(data)
        }else {
          this.message=''
        }
      })
    }
  },
}
</script>

<style scoped>
.container{
  display: flex;
  position: relative;
  padding: 0;
}
/*.btn{*/
/*  margin-top: 15px;*/
/*}*/
.text-field{
  margin-top: -5px;
}
</style>
