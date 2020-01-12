<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <violationList></violationList> -->
    <section class="hero is-primary">
    <div class="hero-body">
      <div class="container">
        <h1 class="title">
          Nuri's Mabasal
        </h1>
      </div>
    </div>
  </section>
    <b-input type="text" v-model="filterText"></b-input>
    <table>
      <tr v-for="violation in filterdViolations" :key="violation.ID" >
        <td><span>{{violation.Name}}</span></td>

        <!-- <b-taglist attached style="display:inline-block;"> -->
        <td>

          <b-tag rounded>{{violation.CatName}}</b-tag>
        </td>
        <td>
          <b-tag rounded type="is-primary" :class="[violation.IsIncluded ? 'is-primary' : 'is-danger']">{{violation.IsIncluded ? 'כלול' : 'לא כלול'}}</b-tag>
        </td>
        
      </tr>
    </table>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import violationList from './components/violationList.vue'

// var violations = [];
// Vue.component();

export default {
  name: 'app',
  created:function(){
      fetch("http://nuri.dooble.ws/nuriviolations").then(res=>{
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
table{
  direction: rtl;
  margin: 24px;
}
td{
  text-align: right !important;
}
</style>
