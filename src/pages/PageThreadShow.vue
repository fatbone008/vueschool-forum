<template>
  <div class="col-large push-top">

      <h1>{{thread.title}}
        <router-link :to="{name: 'ThreadEdit', id: this.id}" class="btn-green btn-small" tag="button">
          Edit Thread
        </router-link>
      </h1>
    <p>
      By <a href="#" class="link-unstyled">Robin</a>, <AppDate :timestamp="thread.publishedAt"></AppDate>
      <span style="float:right; margin-top: 2px;" class="hide-mobile text-faded text-small">3 replies by 3 contributors</span>
    </p>
    <PostList :posts="posts"></PostList>
    <PostEditor :threadId="id"></PostEditor>

  </div>

</template>

<script>
  import PostList from '@/components/PostList'
  import PostEditor from '@/components/PostEditor'
  // import Vue from 'vue'

  export default {
    props: {
      id: {
        required: true,
        type: String
      }
    },
    components: {
      PostList,
      PostEditor
    },
    computed: {
      thread () {
        return this.$store.state.threads[this.id]
      },
      posts () {
        const postIds = Object.values(this.thread.posts)
        return Object.values(this.$store.state.posts)
          .filter(post => postIds.includes(post['.key']))
      }
    }
  }
</script>

<style scoped>

</style>
