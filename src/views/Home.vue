<template>
  <div class="container">
    <post-form @postCreated="addPost" />
    <display-posts :posts="posts" />
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
    }
  },
  created() {
    postService
      .getAllPosts()
      .then((res) => {
        this.posts = res.data
        console.log(this.posts)
      })
      .catch((err) => console.error(err))
  }
}
</script>


