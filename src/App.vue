<template>
<div class="container">
  <Tags v-model="tags" color="success"/>
  {{tags}}
  <hr>
    <Tags v-model="tags2"/>
  {{tags2}}
    <hr>
    <Tags v-model="tags3" color="danger"/>
  {{tags3}}
</div>
  
</template>

<script>
import Tags from './components/Tags'
export default {
  components:{
    Tags,
  },
  data(){
    return{
      tags : "Deneme,test, Success theme",
      tags2 : "Primary, Default theme",
      tags3 : "Danger deneme, danger theme"
    }
  }
};
</script>

<style lang="scss" scoped>
* {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-weight: 700;
}
</style>
