<template>
  <div class="forum-container">
    <div class="col-full push-top">

      <div class="forum-header">
        <div class="forum-details">
          <h1>{{forum.name}}</h1>
          <p class="text-lead">{{forum.description}}</p>
        </div>
        <!--<a href="new-thread.html" class="btn-green btn-small">Start a thread</a>-->
        <router-link :to="{name: 'ThreadCreate', params: {forumId: this.forum['.key']}}" class="btn-green btn-small">Start a thread</router-link>
      </div>
    </div>



    <div class="col-full push">

      <ThreadList :threads="threads"></ThreadList>

    </div>

  </div>
</template>

<script>
  import ThreadList from '@/components/ThreadList'

  export default {
    name: 'page-forum',
    components: {
      ThreadList
    },
    props: {
      id: {
        required: true,
        tyep: String
      }
    },
    computed: {
      forum () {
        return this.$store.state.forums[this.id]
      },
      threads () {
        return Object.values(this.$store.state.threads)
          .filter(thread => thread.forumId === this.id)
      }
    }
  }
</script>

<style scoped>
  .forum-container {
    width: 100%;
  }
</style>
