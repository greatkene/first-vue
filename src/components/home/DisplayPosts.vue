<template>
  <div class="row">
    <div class="col s6" v-for="(post, index) in posts" :item="post" :index="index" :key="post.id">
      <div class="card">
        <div class="card-content">
          <p class="card-title">{{ post?.title }}</p>
          <p class="timestamp">{{ formatDate(post?.createdAt) }}</p>
          <p>
            {{ post.body }}
          </p>
          <div class="card-action">
            <a class="edit-btn" @click="editPost(post)">Edit</a>
            <a class="delete-btn" @click="$emit('deletePost', post?.id)">Delete</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PostList',
  props: {
    posts: {
      type: Array,
      required: true
    }
  },
  methods: {
    editPost(post) {
      this.$emit('editPost', post)
    },
    formatDate(date) {
      const formattedDate = new Date(date)
      const day = formattedDate.getDate()
      const month = formattedDate.getMonth() + 1
      const year = formattedDate.getFullYear()

      return `${day}-${month}-${year}`
    }
  }
}
</script>

<style scoped>
.card .card-content .card-title {
  margin-bottom: 0;
}
.card .card-content p.timestamp {
  color: #999;
  margin-bottom: 10px;
}
.edit-btn {
  cursor: pointer;
}
.delete-btn {
  color: red !important;
  cursor: pointer;
}
</style>
