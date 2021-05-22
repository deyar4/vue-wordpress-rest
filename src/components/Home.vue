<template>
  <main>
  <h1> hello </h1>

  </main>
</template>

<script>
import PostItem from '@/components/template-parts/PostItem'
import Pagination from '@/components/template-parts/Pagination'

export default {
  name: 'Home',
  components: {
    PostItem,
    Pagination
  },
  props: {
    page: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      request: {
        type: 'posts',
        params: { 
          per_page: this.$store.state.site.posts_per_page,
          page: this.page
        }, 
        showLoading: true 
      },
      totalPages: 0
    }
  },
  computed: {
    posts() {
      return this.$store.getters.requestedItems(this.request)
    }
  },
  methods: {
    getPosts() {
      return this.$store.dispatch('getItems', this.request)
    },
    setTotalPages() {
      this.totalPages = this.$store.getters.totalPages(this.request)
    }
  },
  created() {
    this.getPosts().then(() => this.setTotalPages())
  }
}
</script>
