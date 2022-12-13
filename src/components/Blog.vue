<template>
  <main class="blog" :class="{ 'blog--reading': this.post }">
    <a href="#modal1">Добавить</a>
    <a href="#modal2">дщд</a>
    <a href="#modal3">lol</a>
    <button @click="$router.push('#modal3')">lol</button>

  <div v-show="showFirst">
    <div id="modal1" ref="my-modal" class="modal">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h3 class="modal-title"> {{showFirst}} Helllooooo1</h3>
            <a href="#close" title="Close" class="close">×</a>
          </div>
        </div>
      </div>
    </div>
  </div>

    <div id="modal2" class="modal">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h3 class="modal-title"> Helllooooo2</h3>
            <a href="#close" title="Close" class="close">×</a>
          </div>
        </div>
      </div>
    </div>

    <div id="modal3" class="modal">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h3 class="modal-title"> Helllooooo3</h3>
            <a href="#close" title="Close" class="close">×</a>
          </div>
        </div>
      </div>
    </div>

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
      showFirst: true
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

  mounted() {
    this.$getResource('blog')
      .then(x => {
        // use pace hook to know when rendering is ready
      })
  }
}
</script>
