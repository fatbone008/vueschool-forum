<template>
  <div class="col-full push-top">

    <h1>Create new thread in <i>{{forum.name}}</i></h1>

    <ThreadEditor @save="save" @cancel="cancel"></ThreadEditor>
    <!--<form @submit.prevent="save">-->
    <!--<div class="form-group">-->
    <!--<label for="thread_title">Title:</label>-->
    <!--<input v-model="title" type="text" id="thread_title" class="form-input" name="title">-->
    <!--</div>-->

    <!--<div class="form-group">-->
    <!--<label for="thread_content">Content:</label>-->
    <!--<textarea v-model="text" id="thread_content" class="form-input" name="content" rows="8" cols="140"></textarea>-->
    <!--</div>-->

    <!--<div class="btn-group">-->
    <!--<button @click.prevent="cancel" class="btn btn-ghost">Cancel</button>-->
    <!--<button class="btn btn-blue" type="submit" name="Publish">Publish </button>-->
    <!--</div>-->
    <!--</form>-->
  </div>
</template>

<script>
  import ThreadEditor from '@/components/ThreadEditor'

  export default {
    components: {
      ThreadEditor
    },
    props: {
      forumId: {
        type: String,
        required: true
      }
    },
    methods: {
      save ({title, text}) {
        // dispatch
        this.$store.dispatch('createThread', {forumId: this.forum['.key'], title, text})
          .then(thread => {
            this.$router.push({name: 'ThreadShow', params: {id: thread['.key']}})
          })
      },
      cancel () {
        this.$router.push({name: 'forum', params: {id: this.forum['.key']}})
      }
    },
    computed: {
      forum () {
        return this.$store.state.forums[this.forumId]
      }
    }
  }
</script>

<style scoped>

</style>
