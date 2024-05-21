<template>
  <div class="post-container">
    <div class="dropdown-container">
      <select class="select-dropdown" v-model="selectedCategory" @change="fetchPosts">
        <option value="">All Categories</option>
        <option v-for="category in categories" :key="category.slug" :value="category.slug">
          {{ category.name }}
        </option>
      </select>
    </div>
    <div class="posts">
      <PostCard v-for="post in posts" :key="post.slug" :post="post" />
    </div>
    <button @click="loadMore">Load More</button>
  </div>
</template>

<script>
import axios from 'axios';
import PostCard from './PostCard.vue';

export default {
  components: {
    PostCard
  },
  data() {
    return {
      posts: [],
      categories: [],
      selectedCategory: '',
      page: 1
    };
  },
  methods: {
    async fetchPosts() {
      const categoryQuery = this.selectedCategory ? `&category=${this.selectedCategory}` : '';
      const response = await axios.get(`https://public-api.wordpress.com/rest/v1.1/sites/107403796/posts/?fields=slug,categories,post_thumbnail,title,date&number=20&page=${this.page}${categoryQuery}`);
      if (this.page === 1) {
        this.posts = response.data.posts;
      } else {
        this.posts = [...this.posts, ...response.data.posts];
      }
    },
    async fetchCategories() {
      const response = await axios.get('https://public-api.wordpress.com/rest/v1.1/sites/107403796/categories');
      this.categories = response.data.categories;
    },
    loadMore() {
      this.page += 1;
      this.fetchPosts();
    }
  },
  created() {
    this.fetchPosts();
    this.fetchCategories();
  },
  watch: {
    selectedCategory() {
      this.page = 1;
      this.fetchPosts();
    }
  }
};
</script>

<style scoped>
.post-container {
  padding: 20px;
}

.dropdown-container {
  display: flex;
  justify-content: flex-start;
  margin-bottom: 20px;
}

.select-dropdown {
  width: 100%;
  max-width: 300px;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #fff;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  margin-left: 8px;
}

.select-dropdown:focus,
.select-dropdown:hover {
  border-color: #007bff;
  cursor: pointer;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
  outline: none;
}

.select-dropdown option {
  padding: 6px;
  font-size: 16px;
}

.posts {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.post-card {
  flex: 0 1 calc(25% - 20px);
  margin-bottom: 20px;
  padding: 15px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #fff;
  box-sizing: border-box;
}

.post-card img {
  width: 100%;
  height: auto;
  border-radius: 5px 5px 0 0;
}

.post-info {
  padding: 10px 0;
}

.post-info h2 {
  font-size: 1.1em;
  margin: 0;
}

.post-info p {
  font-size: 0.9em;
  color: #777;
  margin: 0;
}

button {
  width: 100px;
  padding: 10px;
  font-size: 16px;
  color: #fff;
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 20px;
}

button:hover {
  background-color: #0056b3;
}

@media (max-width: 1200px) {
  .post-card {
    flex-basis: calc(33.33% - 20px);
  }
}

@media (max-width: 992px) {
  .post-card {
    flex-basis: calc(50% - 20px);
  }
}

@media (max-width: 768px) {
  .posts {
    justify-content: center;
  }

  .post-card {
    flex-basis: calc(50% - 20px);
  }
}

@media (max-width: 576px) {
  .post-card {
    flex-basis: calc(100% - 20px);
  }
}
</style>
