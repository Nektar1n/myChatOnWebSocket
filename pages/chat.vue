<template>
  <div class="container">
    <ul>
      <li v-for="mes in $store.state.messages" :key="mes.text">
        {{mes.text}}
      </li>
    </ul>
  </div>

</template>

<script>
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
  }
}
</script>

<style scoped>

</style>
