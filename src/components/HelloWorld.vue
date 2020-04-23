<template>
  <div class="hello">
    <button v-on:click="doesNotWork">DOES NOT WORK</button>
    <button v-on:click="works">WORKS</button>
    
    {{v}}   
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { Store } from 'vuex';
import { testState as test, TestStateInterface } from "../store/TestState" 
import { namespace } from "vuex-class"

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;
  doesNotWork() {
    const store = this.$store.state.test;
    test.mutations.mutateTestVal(store, "new value (not works)");
  }
  works() {    
    this.$store.commit("test/mutateTestVal", "new value (works)");    
  }
  get v() : string {
    const store = this.$store.state.test;
    return test.getters.testValGetter(store);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
