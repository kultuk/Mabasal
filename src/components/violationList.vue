<template>
    <div class="">
        <input type="text">
        <ul >
            <li v-for="violation in violations" :key="violation.ID" style="color:red;">
                {{violation.Name}}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
  name: 'violationList',
  props: {
    violations: Array
  },
  data: function(){
      return {filterText:''};
  }
}
</script>