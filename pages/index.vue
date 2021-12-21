<template>
  <div>
    <ul>
      <li v-for="post in posts" :key="post.id">
        {{ post.title }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      posts: [],
    };
  },
  mounted() {
    this.fetchPosts();
  },
  methods: {
    async fetchPosts() {
      this.posts = await this.$axios.$get('/posts');
    },
  },
};
</script>
