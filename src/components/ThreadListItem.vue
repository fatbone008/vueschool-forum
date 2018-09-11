<template>

  <div class="thread">
    <div>
      <p>
        <a :href="`/thread/${thread['.key']}`">{{thread.title}}</a>
        <router-link :to="{name: 'ThreadShow', params: {id: thread['.key']}}">
          {{thread.title}}
        </router-link>
      </p>
      <p class="text-faded text-xsmall">
        By <a href="#">Joseph Kerr</a>, <AppDate :timestamp="thread.publishedAt"></AppDate>.
      </p>
    </div>

    <div class="activity">
      <p class="replies-count">
        {{repliesCount}} replies
      </p>

      <!--<img class="avatar-medium"-->
           <!--src="http://i0.kym-cdn.com/photos/images/facebook/000/010/934/46623-batman_pikachu_super.png" alt="">-->

      <div>
      <p class="text-xsmall">
      <a href="#">{{user.name}}</a>
      </p>
      <p class="text-xsmall text-faded">2 hours ago</p>
      </div>
    </div>
  </div>

</template>

<script>
  import {countObjectProperties} from '../utils'

  export default {
    name: 'thread-list-item',
    props: {
      thread: {
        requred: true,
        type: Object
      }
    },
    computed: {
      repliesCount () {
        return countObjectProperties(this.thread.posts) - 1
      },
      user () {
        return this.$store.state.users[this.thread.userId]
      }
    }
  }
</script>

<style scoped>

</style>
