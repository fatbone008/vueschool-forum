<template>

  <div class="col-full push-top">

    <h1>Editing<i>{{thread.title}}</i></h1>

    <ThreadEditor :title="thread.title" :text="text" @save="save" @cancel="cancel"></ThreadEditor>
  </div>
</template>

<script>
  import ThreadEditor from '@/components/ThreadEditor'

  export default {
    components: {
      ThreadEditor
    },
    props: {
      id: {
        type: String,
        required: true
      }
    },
    methods: {
      save ({title, text}) {
        // dispatch
        this.$store.dispatch('updateThread', {id: this.id, title, text})
          .then(thread => {
            // console.log('应该拿到的thread:', thread)
            this.$router.push({name: 'ThreadShow', params: {id: this.id}})
          })
      },
      cancel () {
        this.$router.push({name: 'forum', params: {id: this.id}})
      }
    },
    computed: {
      thread () {
        return this.$store.state.threads[this.id]
      },

      text () {
        return this.$store.state.posts[this.thread.firstPostId].text
      }
    }
  }
</script>

<style scoped>

</style>
