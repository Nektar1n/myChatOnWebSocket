<template>
  <div class="c-wrap">
    <div class="c-chat">
<!--      <ul>-->
<!--        <li v-for="mes in $store.state.messages" :key="mes.text">-->
<!--          {{mes.text}}-->
<!--        </li>-->
<!--      </ul>-->
      <message
        v-for="mes in $store.state.messages" :key="mes.text"
        :name="mes.name"
        :text="mes.text"
        :owner="mes.id===$store.state.user.id"
      />
    </div>
    <div class="c-form">
      <ChatForm/>
    </div>
  </div>

</template>

<script>
import Message from "../components/Message";
import ChatForm from "../components/ChatForm";
export default {
  name: "chat",
  layout:'default',
  head(){
    return{
      title:`Ты в комнате ${this.$store.state.user.room}`
    }
  },
  middleware:['chat'],
  data(){
    return{
      userName:'',
      num:8983989,
    }
  },
  mounted() {
    this.userName=this.$store.state.user.name
  },
  components:{Message,ChatForm}
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
