<template>
  <div id="app">
    <section class="hero is-info">
    <div class="hero-body">
      <div class="container">
        <h1 class="title">
          מה בסל
        </h1>
      </div>
    </div>
  </section>
    <b-input type="text" v-model="filterText" custom-class="search-bar" placeholder="הכנס שם עבירה"></b-input>
    <table>
      <tr v-for="violation in filterdViolations" :key="violation.ID" >
        <td><span>{{violation.Name}}</span></td>
        <td>

          <b-tag rounded>{{violation.CatName}}</b-tag>
        </td>
        <td>
          <b-tag rounded type="is-info" :class="[violation.IsIncluded ? 'is-info' : 'is-danger']">{{violation.IsIncluded ? 'כלול' : 'לא כלול'}}</b-tag>
        </td>
        
      </tr>
    </table>
    <img src="./assets/folivora-logo.png" alt="Folivora Logo" class="logo-img" @click="rollCredits">
  </div>
</template>

<script>
import { ToastProgrammatic as Toast } from 'buefy';

export default {
  name: 'app',
  created:function(){
      fetch("https://nuri.dooble.ws/nuriviolations").then(res=>{
          res.json().then(data=>{
              // console.log(data)
              this.violations = data;
              this.filterdViolations = this.violations.map(x=>x)
          })
      })
  },
  data: function(){
    return {violations:[], filterText:'',filterdViolations: []}
  },
  watch: {
    filterText:function(){
      // console.log(this.filterText)
      this.filterViolations(this.filterText);
    }
  },
  methods: {
    filterViolations : function(filter){
      // var filter = this.filterText;
      this.filterdViolations = this.violations.filter(function(violation){
        // console.log(self.filterText)
        return (!filter || (violation.Name || '').indexOf(filter) != -1);
      })
    },
    rollCredits(){
      Toast.open("נוצר על ידי נוריאל שקורי וסהר זהבי");
    }
  },
  components: {
    // violationList
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}
.search-bar{
  text-align: right;
  color: orange !important;
  border-color: orange !important;  
}
.logo-img{
  height: 100px;
}
table{
  direction: rtl;
  margin: 24px;
  width: 94%;
}
td{
  text-align: right !important;
}
</style>
