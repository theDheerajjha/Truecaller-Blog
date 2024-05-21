<template>
    <div>
      <Header :showHeaderImage="true" />
      <PostList />
    </div>
  </template>
  
  <script>
  import PostList from '@/components/PostList.vue';
  import Header from '@/components/Header.vue';

  
  export default {
    components: {
      PostList,
      Header
    }
  };
  </script>
  