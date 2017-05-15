<template>
  <div class="hello">
    <h1 :class='status'>{{target.health}}</h1>
    <img :src="myPic">
    <button v-for="atk in attacks" @click="attack(atk.name)">{{atk.name}}</button>
    <button v-for="itm in items" @click="giveItem(itm.name)">{{itm.name}}</button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      target: { 
        health: 100,
        items: []
      },
      status: 'green',
      myPic: "http://unsplash.it/200/200",
      attacks:{
        slap: { val: 1, name: 'slap' },
        punch: {val: 4, name: 'punch'},
        DIE: {val: 1000, name: 'DIE'}
      },
      items:{
        armor: { val: .3, name: 'armor'},
        shield: { val: .5, name: 'shield'}
      }
    }
  },
  methods:{
    attack(dmgType){

      var totalMods = 1
      for(var i = 0; i < this.target.items.length; i++){
        var item = this.target.items[i]
        totalMods += item.val
      }

      var amt = this.attacks[dmgType].val / totalMods
      console.log(amt)
      if(amt){
        this.target.health -= Math.round(amt)
        this.update()
      }
    },
    update(){
      if(this.health < 0){ this.health = 0}
      if(this.health < 60 && this.health > 40){
        this.status = 'yellow'
        this.myPic = "http://unsplash.it/g/200/200"
      }else if(this.health < 40 && this.health > 0){
        this.status = 'black'
        this.myPic = "http://unsplash.it/g/200/200"
      }
    },
    giveItem(itmName){
      if(this.items[itmName]){
        this.target.items.push(this.items[itmName])
        console.log('Target gains a ', itmName)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1{
  background: green;
  color: white;
}
.green{
  background: green;
}
.yellow{
  background: yellow;
}
.black{
  background: black;
}
</style>
