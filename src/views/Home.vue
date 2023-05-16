<template>
  <div class="container">
    <post-form @postCreated="addPost" />
    <display-posts :posts="posts" @deletePost="deletePost" />
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
      posts: []
    }
  },
  methods: {
    addPost(post) {
      this.posts.unshift(post)
    },
    editPost(post) {
      console.log(post)
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


