<template>
  <div class="post-card" @click="goToPost">
    <img :src="post.post_thumbnail.URL" alt="Thumbnail" />
    <div class="post-info">
      <h2>{{ post.title }}</h2>
      <p class="post-date">{{ formatDate(post.date) }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['post'],
  methods: {
    goToPost() {
      this.$router.push(`/post/${this.post.slug}`);
    },
    formatDate(date) {
      const now = new Date();
      const postDate = new Date(date);
      const diff = Math.abs(now - postDate) / 1000;
      const days = Math.floor(diff / 86400);
      if (days > 1) return `${days} days ago`;
      const hours = Math.floor(diff / 3600);
      if (hours > 1) return `${hours} hours ago`;
      const minutes = Math.floor(diff / 60);
      if (minutes > 1) return `${minutes} minutes ago`;
      return `${diff} seconds ago`;
    }
  }
};
</script>

<style scoped>
.post-card {
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 10px;
  margin: 10px;
  cursor: pointer;
  width: calc(25% - 20px);
  max-width: 300px;
  display: flex;
  flex-direction: column;
  align-items: center;
  box-sizing: border-box;
}

.post-card img {
  width: 100%;
  height: auto;
  border-radius: 5px 5px 0 0;
}

.post-info {
  text-align: center;
  padding: 10px;
}

.post-info h2 {
  font-size: 1.2em;
  margin-bottom: 5px;
}

.post-date {
  font-size: 0.9em;
  color: #777;
}
</style>
