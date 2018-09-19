<template>

  <div class="post">

    <div class="user-info">
      <a href="#" class="user-name">{{user.name }}</a>

      <a href="#">
        <img class="avatar-large" :src="user.avatar" alt="">
      </a>

      <p class="desktop-only text-small">{{userPostsCount}} posts</p>

    </div>

    <div class="post-content">
      <div v-if="!editing">
        {{post.text}}
      </div>
      <div v-else>
        <PostEditor :post="post"></PostEditor>
      </div>
    </div>

    <div class="post-date text-faded" >
      <AppDate :timestamp="post.publishedAt"></AppDate>
    </div>

  </div>
</template>

<script>
  import {countObjectProperties} from '../utils'
  import PostEditor from '@/components/PostEditor'

  export default {
    name: 'post-list-item',
    components: {
      PostEditor
    },
    data () {
      return {
        editing: true
      }
    },
    props: {
      post: {
        required: true,
        type: Object
      }
    },
    computed: {
      user () {
        return this.$store.state.users[this.post.userId]
      },
      userPostsCount () {
        // const postIds = this.user.postIds
        // const postIdsArray = Object.keys(postIds)
        // return postIdsArray.length
        return countObjectProperties(this.user.posts)
        // return Object.keys(this.user.posts).length
      }
    }
  }
</script>

<style scoped>

</style>
