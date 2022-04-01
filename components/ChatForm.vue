<template>
        <v-flex xs12>
          <v-text-field
            v-model="message"
            @keydown.enter="send"
            label="Введите сообщение"
          ></v-text-field>
        </v-flex>
</template>

<script>
export default {
  name:"ChatForm",
  data: () => ({
    message: '',
  }),
  methods: {
    send(){
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

</style>
