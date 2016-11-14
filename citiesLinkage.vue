<template>
  <div class="citiesLinkage">
      <select class="provinces" v-model="province"><option v-for="(item,key) in provincesName" :value="key">{{item}}</option></select><select class="citys" v-model="city"><option v-for="(item,key) in citysName" :value="key">{{item}}</option></select><select class="countys" v-model="county"><option v-for="(item,key) in countysName" :value="key">{{item}}</option></select>
  </div>
</template>

<script>
import { addrobj, addrname } from '../assets/addr.js'

export default {
  data () {
    return {
      province:10,
      city:20,
      county:31
    }
  },
  computed:{
         provincesName:function(){
             var provinceName={};
             for(var i in addrobj){
                  provinceName[i]=addrname[i];
             }
             return provinceName
         },
         citysName:function(){
             var cityName={};
             for(var i in addrobj[this.province]){
                 cityName[i]=addrname[i]
             }
             return cityName
         },
         countysName:function(){
             var countyName={};
             for(var i in addrobj[this.province][this.city]){
                 var county=addrobj[this.province][this.city][i];
                 countyName[county]=addrname[county]
             }
             return countyName
         },
    },
    watch:{
        'province':function(n,o){
            if(n!=o) this.city=Object.getOwnPropertyNames(this.citysName)[0];
        },
        'city':function(n,o){
            if(n!=o) this.county=Object.getOwnPropertyNames(this.countysName)[0];
        }
    }
}
</script>


<style scoped>

</style>
