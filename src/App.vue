<template>
  <div class="container" id="app">
    
    <SourceSelection v-on:sourceChanged="sourceChanged"></SourceSelection>

    <Newslist v-bind:source="source"></Newslist>

  </div>
</template>

<script>
import Newslist from './components/Newslist';
import SourceSelection from './components/SourceSelection';

export default {
  name: 'app',
  components: {
    Newslist,
    SourceSelection,
  },
  data() {
    return {
      source: '',
    };
  },
  methods: {
    sourceChanged: function sourcechanged(source) {
      this.source = source;
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  /*color: #2c3e50;*/
  /*margin-top: 60px;*/
}
</style>
