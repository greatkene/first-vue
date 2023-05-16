<template>
  <div class="row">
    <div class="col s6" v-for="(post, index) in posts" :item="post" :index="index" :key="post.id">
      <div class="card">
        <div class="card-content">
          <p class="card-title">{{ post?.title }}</p>
          <p class="timestamp">{{ post?.createdAt }}</p>
          <p>
            {{ post.body }}
          </p>
          <div class="card-action">
            <a href="#">Edit</a>
            <a href="#" class="delete-btn">Delete</a>
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
.delete-btn {
  color: red !important;
}
</style>
