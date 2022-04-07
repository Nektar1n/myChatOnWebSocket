<template>
<div class="user">
  <h1>user</h1>
<!--  <h1>{{$route.params.user}}</h1>-->
<!--  <h1>{{ $route.query }}</h1>-->
  <h1>{{user}}</h1>
</div>
</template>

<script>
export default {
  layout:'chat-layout',
  name: "aboutUser",
  head(){
    return{
      title:`${this.$route.params.user}`
    }
  },
  data(){
    return{
      user:null
    }
  },
  mounted() {
    console.log(this.$route.query)
    console.log(this.$store.state.users)
    this.$store.state.users.map((item)=>{
      if (item.name===this.$route.query.name){
        this.user=item
      }
      // else if (item.name!==this.$route.query.name){
      //   this.$router.push({path:'/chat'})
      // }
      return this.user
    })

  },
  middleware:['_user']
}
</script>

<style scoped>

</style>
