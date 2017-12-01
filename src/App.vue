
<template>
<scroller>

<div>
<text class="minibar">Vuenos Aires</text>
</div>

<div class="wrapper">

<div style="margin-top:20px; align-items:center">
<image :src="logoUrl" class="logo"></image>
</div>
<div>

<text class="description">
Vuenos Aires es un meetup donde nos 
enfocamos en aprender, enseñar y difundir todo 
lo que tenga que ver con el ecosistema de </text>
<text class="description" style="color:#3eb882">Vue.js </text>
</div>
    
<div v-if="!meetup" style="flex-direction:column; align-items:center">
<text style="margin-top: 30px">No hay Meetup Programada</text>  
<image style="width:50px; height:50px; margin-top:20px" src="https://s3-sa-east-1.amazonaws.com/vuenos-aires/sad.png"></image>
</div>

<div v-else style="flex-direction:column; align-items:center">
  <text style="margin-top: 30px">Tenemos Meetup</text>  
  <image style="width:50px; height:50px; margin-top:20px" src="https://s3-sa-east-1.amazonaws.com/vuenos-aires/meetup.png"></image>
  <text style="margin-top:30px">{{name}}</text>
  <text style="margin-top:10px">{{address}}</text>
  <text style="margin-top:10px">{{date}} {{time}}</text>
</div>
</div>

<div style="align-items: center; margin-top:50px">
  <text>Con el apoyo de</text>
</div>

<div style="flex-direction:row; justify-content:space-between; margin-top:50px; margin-left:10px; margin-right:10px">
<image style="width:200px; height:100px;" src="https://s3-sa-east-1.amazonaws.com/vuenos-aires/vuejsfeed.png"></image>
<image style="width:200px; height:100px;" src="https://s3-sa-east-1.amazonaws.com/vuenos-aires/frontend-masters.png"></image>
<image style="width:200px; height:100px;" src="https://s3-sa-east-1.amazonaws.com/vuenos-aires/htmlburger.png"></image>
</div>

<div style="flex-direction:row; justify-content:space-between; margin-top:100px; margin-left:10px; margin-right:10px">
<image style="width:200px; height:100px;" src="https://s3-sa-east-1.amazonaws.com/vuenos-aires/jetbrains.png"></image>
<image style="width:200px; height:100px;" src="https://s3-sa-east-1.amazonaws.com/vuenos-aires/platzi.png"></image>
<image style="width:200px; height:100px;" src="https://s3-sa-east-1.amazonaws.com/vuenos-aires/tmvuejs2.png"></image>
</div>



</scroller>

</template>


<style>
  .minibar {font-size: 70px; color: #3eb882; text-align: center}
  .description {text-align:center;color: #445b71}
  .wrapper {margin-top: 30px; background-color: #f4f4f4;}
  .logo { width: 250px; height: 250px; }
</style>

<script>
  const stream = weex.requireModule('stream')
  export default {
    data () {
      return {
        logoUrl: 'https://s3-sa-east-1.amazonaws.com/vuenos-aires/vuenosaires.png',
        name: '',
        address:'',
        date:'',
        time:'',
        meetup: false 
    }
    },
    methods: {
      getStarCount (callback) {
        return stream.fetch({
          method: 'GET',
          type: 'json',
          url: 'https://api.meetup.com/vuenos-aires/events?key=6161702b7f552bb5e42633f4c62692a&sign=true&photo-host=public&page=20'
        }, callback)
      }
    },
    created () {
      this.getStarCount(res => {
        console.log(res.data)
        if (res.data.length !== 0){
          this.meetup = true
          this.name = res.data.venue.name
          this.address = res.data.venue.address_1
          this.date = res.data.local_date
          this.time = res.data.local_time
        }
      })
    } 
  }
</script>
