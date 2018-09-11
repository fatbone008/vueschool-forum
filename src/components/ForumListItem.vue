<template>

  <div class="forum-listing">
    <div class="forum-details">
      <router-link :to="{name:'forum', params: {id: forum['.key']}}" class="text-xlarge">{{forum.name}}</router-link>
      <p>{{forum.description}}</p>
    </div>

    <div class="threads-count">
      <p class="count">{{threadsCount}}</span>
        {{threadsCount === 1 ? 'thread' : 'threads'}}
      </p>
    </div>

    <div class="last-thread">
      <!--TODO: implement laten-->
    </div>
  </div>
</template>

<script>
  import {countObjectProperties} from '@/utils'

  export default {
    props: {
      forum: {
        required: true,
        type: Object
      }
    },
    computed: {
      threadsCount () {
        return countObjectProperties(this.forum.threads)
      }
    }
  }
</script>

<style scoped>

</style>
