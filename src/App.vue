<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>This is my auto-suggestion demo</h1>
    <h5>VueJS sux</h5>
    <input @input="suggestions = [$event.target.value]">
    <ul>
      <li v-for="item in suggestionList" :key="item">
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import {
  CollapsedNode, getFirstNode, getCollapsedTrie, collectTerms,
} from './lib/trie';

@Component({
  components: {
    HelloWorld,
  },
})
export default class App extends Vue {
  private suggestionList: string[] = [];

  private node: CollapsedNode = getCollapsedTrie();

  // private nodeStack: StackDAtum[] = [];

  private lastLength = 0;

  get suggestions(): string[] {
    return this.suggestionList;
  }

  set suggestions(currentTerm: string []) {
    this.suggestionList = collectTerms(getFirstNode(this.node, currentTerm[0]));
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
