<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <label for="tilte">Post</label>
      <input type="text" name="title" v-model="form.title" ref="title" />
      <button type="submit">Add</button>
    </form>
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
      form: {
        title: '',
      },
    };
  },
  mounted() {
    this.fetchPosts();
  },
  methods: {
    async handleSubmit() {
      await this.$axios.$post('/posts', this.form);
      await this.fetchPosts();

      this.$refs.title.focus();
      this.form.title = '';
    },
    async fetchPosts() {
      this.posts = await this.$axios.$get('/posts');
    },
  },
};
</script>
