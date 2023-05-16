<template>
  <div class="container">
    <post-form @postCreated="addPost" :editingPost="editingPost" />
    <display-posts :posts="posts" @deletePost="deletePost" @editPost="editPost" />
  </div>
</template>

<script>
import DisplayPosts from '../components/home/DisplayPosts.vue'
import PostForm from '../components/home/PostForm.vue'
import PostService from '../services/post.service'

const postService = new PostService()

export default {
  components: { DisplayPosts, PostForm },
  name: 'Home',
  data() {
    return {
      posts: [],
      editingPost: null
    }
  },
  methods: {
    addPost(post) {
      if (this.posts.find((p) => p.id === post.id)) {
        const index = this.posts.findIndex((p) => p.id === post.id)
        this.posts.splice(index, 1, post)
      } else this.posts.unshift(post)
    },
    editPost(post) {
      this.editingPost = { ...post }
    },
    deletePost(id) {
      postService
        .deletePost(id)
        .then(() => {
          this.posts = this.posts.filter((p) => p.id !== id)
        })
        .catch((err) => console.error(err))
    }
  },
  created() {
    postService
      .getAllPosts()
      .then((res) => {
        this.posts = res.data
      })
      .catch((err) => console.error(err))
  }
}
</script>
