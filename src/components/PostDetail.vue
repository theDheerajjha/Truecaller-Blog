<template>
  <div class="post-detail">
    <div class="post-detail-img">
      <img :src="post.featured_image" alt="Featured Image" />
      <h1>{{ post.title }}</h1>
    </div>
    <p>By {{ post.author.name }} on {{ formatDate(post.date) }}</p>
    <div class="post-content" v-html="post.content"></div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      post: {}
    };
  },
  methods: {
    async fetchPost() {
      const { slug } = this.$route.params;
      const response = await axios.get(`https://public-api.wordpress.com/rest/v1.1/sites/107403796/posts/slug:${slug}?fields=featured_image,title,author,content,date`);
      this.post = response.data;
    },
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      return new Date(date).toLocaleDateString(undefined, options);
    }
  },
  created() {
    this.fetchPost();
  }
};
</script>

<style scoped>
.post-detail {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  box-sizing: border-box;
}

.post-detail-img {
  width: 100%;
  text-align: center;
  margin-bottom: 20px;
}

.post-detail-img img {
  width: 100%;
  height: auto;
  max-width: 100%;
  border-radius: 10px;
}

.post-detail-img h1 {
  margin-top: 20px;
  font-size: 2em;
  line-height: 1.2;
}

p {
  text-align: center;
  color: #555;
  margin-bottom: 20px;
}

.post-content {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  line-height: 1.6;
  font-size: 1.1em;
}

@media (max-width: 768px) {
  .post-detail {
    padding: 10px;
  }

  .post-detail-img h1 {
    font-size: 1.8em;
  }

  .post-content {
    width: 90%;
    font-size: 1em;
  }
}

@media (max-width: 480px) {
  .post-detail-img h1 {
    font-size: 1.5em;
  }

  .post-content {
    width: 100%;
    font-size: 0.95em;
  }
}
</style>
