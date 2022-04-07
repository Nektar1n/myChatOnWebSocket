<template>
    <div class="c-wrap">
      <div class="c-chat"  ref="chatWindow">
        <message
          ref="mesWindow"
          v-for="mes in updateMessages" :key="mes.text"
          :name="mes.name"
          :text="mes.text"
          :owner="mes.id===$store.state.user.id"
        />
      </div>
      <div class="c-form">
        <ChatForm @scrollBottom="scrollBottom"/>
      </div>
    </div>
</template>

<script>
import Message from "../../components/Message";
import ChatForm from "../../components/ChatForm";
import AboutUser from "./_user";
export default {
  name: "chat",
  layout:'chat-layout',
  head(){
    return{
      title:`Ты в комнате ${this.$store.state.user.room}`
    }
  },
  methods:{
    scrollBottom(){
      console.log('hello' +this.$refs.chatWindow.pageYOffset)
      setTimeout(()=>{
        // this.$refs.chatWindow.scrollTop=this.$refs.chatWindow.scrollHeight+40
        this.$refs.chatWindow.scrollTo({top:this.$refs.chatWindow.scrollHeight+40
        ,behavior:"smooth"})
      },10)

    }
  },
  middleware:['chat'],
  data(){
    return{
      messages:[]
    }
  },
  computed:{
    updateMessages(){
      return this.messages=this.$store.state.messages
    }
  },
  watch:{
    messages(){
      setTimeout(()=>{
        // this.$refs.chatWindow.scrollTop=this.$refs.chatWindow.scrollHeight+40
        this.$refs.chatWindow.scrollTo({top:this.$refs.chatWindow.scrollHeight+40
          ,behavior:"smooth"})
      },10)
    }
  },
  mounted() {
    // this.$refs.element.scrollTop=this.$refs.element.scrollHeight
    // const objEl=document.getElementById('element')
    // objEl.scrollTop=objEl.scrollHeight
  },
  components:{AboutUser, Message,ChatForm}
}
</script>

<style scoped>
  .c-wrap{
    height: 100%;
    position: relative;
    overflow: hidden;
  }
  .c-chat{
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 80px;
    padding: 1rem;
    overflow-y: auto;
  }

  .c-form{
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 1rem;
    height: 80px;
    background: #212121;
  }

</style>
