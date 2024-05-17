<template>
  <h1 class='mb-6 text-4xl font-bold text-gray-800'>Search</h1>
  <div class="search-container">
    <div class="relative input-wrapper">
      <input class='px-3 py-1 sm:w-[600px] w-full mb-4' type="text" v-model="query" placeholder="Search..."  />
      <span class='absolute sm:left-[570px] top-[4px] right-[10px] cursor-pointer' v-if="query"  @click="clearQuery">✕</span>
    </div>
    <p  v-if="query"><span class='font-bold'>{{ filteredArticles.length }} {{ filteredArticles.length === 1 ? 'post' : 'posts' }}</span>{{ filteredArticles.length === 1 ? ' was' : ' where' }} found</p>
    <div v-if="query">
      <div class='mt-16 article' v-for="blog in filteredArticles" :key="blog.id" >
        <h3 class='mb-1 text-2xl font-bold' v-html="highlight(blog.header)"></h3>
        <p class='mb-2 font-normal' v-html="highlight(blog.date)"></p>
        <p v-html="highlight(blog.description)"></p>
        <hr class='text-[#E7E7E7] mt-2'/>
      </div>
    </div>
  </div>
</template>

<script>
import articles from '../constants.js';

export default {
  data() {
    return {
      query: '',
      articles: articles,
    };
  },
  computed: {
    filteredArticles() {
      if (this.query) {
        const regex = new RegExp(this.query, 'gi');
        return this.articles.filter(blog => regex.test(blog.description) || regex.test(blog.date) || regex.test(blog.header));
      }
      return this.articles;
    }
  },
  methods: {
    clearQuery() {
      this.query = '';
    },
    highlight(text) {
      const regex = new RegExp(this.query, 'gi');
      return text.replace(regex, match => `<span class="bg-[#F8DB5B]">${match}</span>`);
    }
  }
};
</script>
