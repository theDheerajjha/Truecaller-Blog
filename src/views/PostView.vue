<template>
  <div>
    <Header :showHeaderImage="false" />
    <PostDetail />
  </div>
</template>

<script>
import PostDetail from '@/components/PostDetail.vue';
import Header from '@/components/Header.vue';


export default {
  components: {
    PostDetail,
    Header
  }
};
</script>