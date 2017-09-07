<template>
  <div class="newslist">
    <div class="container">
      <ul class="media-list">
        <li class="media" v-for="article in articles">
          <div class="media-left">
            <a v-bind:href="article.url" target="_blank">
              <img v-bind:src="article.urlToImage" alt="image" class="media-object">
            </a>
          </div>
          <div class="media-body">
            <h4 class="media-heading">
              <a v-bind:href="article.url" target="_blank">
                {{article.title}}
              </a>
            </h4>
            <h5><i>by {{article.author}}</i></h5>
            <p>{{article.description}}</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
const apiKey = '6f0bfd8e7e60471a8696a7b05d111f6d';
export default {
  name: 'newslist',
  props: ['source'],
  data() {
    return {
      articles: [],
    };
  },
  methods: {
    updateSource: function updatesource(source) {
      const sourceSelected = source;
      const sourceUrl = `https://newsapi.org/v1/articles?source=${sourceSelected}&apiKey=${apiKey}`;
      this.$http.get(sourceUrl)
        .then((response) => {
          this.articles = response.data.articles;
        });
    },
  },
  created: function initUpdateSource() {
    this.updateSource(this.source);
  },
  watch: {
    source: function watchSource(val) {
      this.updateSource(val);
    },
  },
};
</script>

<style scoped>
  .media-object{
    width: 128px;
    padding: 10px;
  }
  .media{
    border-top: 1px solid lightgray;
    padding-top: 20px;
  }
</style>