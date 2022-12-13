<template>
  <main class="blog" :class="{ 'blog--reading': this.post }">
    <Modal
      v-show="isModalVisible"
      @close="closeModal"
      @continue="continueModal"
    />
    <blog-nav :content="content" :filters="filters" :navs="navs"/>
    <blog-feed :filters="filters"/>
    <blog-post :post="post"/>
    <blog-footer/>
  </main>
</template>

<script>
import BlogNav from './BlogNav'
import BlogFeed from './BlogFeed'
import BlogPost from './BlogPost'
import BlogFooter from './BlogFooter'
import Modal from './Modal';

export default {
  name: 'blog',
  components: { BlogNav, BlogFeed, BlogPost, BlogFooter, Modal },
  resource: 'Blog',
  props: {
    post: String,
    author: String
  },

  data() {
    return {
      navs: 0,
      title: '',
      labels: {
        post: '',
        author: ''
      },
      isModalVisible: true
    }
  },

  computed: {
    content() {
      return { title: this.title, labels: this.labels }
    },
    filters() {
      let filters = {}

      if (this.post) filters.post = this.post
      if (this.author) filters.author = this.author

      return filters
    }
  },

  watch: {
    '$route.name' (to, from) {
      if (to !== from) this.navs++
    }
  },

  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
    continueModal() {
      this.isModalVisible = false;
      setTimeout(() => {
        this.isModalVisible = true;
      }, 200);
    }
  },

  mounted() {
    this.$getResource('blog')
      .then(x => {
        // use pace hook to know when rendering is ready
      })
  }
}
</script>
