<template>
  <div class="sourceSelection">
    <div>
      <div class="jumbotron">
        <h2>
          <span class="glyphicon glyphicon-list-alt"></span>&nbsp;News List
        </h2>
        <h4>Select News Source</h4>
        <select class="form-control" v-on:change="sourceChanged">
          <option value="">Please select news source ...</option>
          <option v-for="source in sources" v-bind:value="source.id">{{source.name}}</option>
        </select>
        <div v-if="source">
          <h6>{{source.description}}</h6>
          <a v-bind:href="source.url" class="btn btn-primary" target="_blank">Go To {{source.name}} Website</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
let i = 0;
export default {
  name: 'sourceSelection',
  data() {
    return {
      sources: [],
      source: '',
    };
  },
  methods: {
    sourceChanged: function sourcechanged(e) {
      for (i = 0; i < this.sources.length; i += 1) {
        if (this.sources[i].id === e.target.value) {
          this.source = this.sources[i];
        }
      }
      this.$emit('sourceChanged', e.target.value);
    },
  },
  created: function sourceinit() {
    this.$http.get('https://newsapi.org/v1/sources?language=en')
      .then((response) => {
        this.sources = response.data.sources;
      });
  },
};
</script scoped>

<style>
  
</style>