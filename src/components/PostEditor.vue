<template>
  <form @submit.prevent="save">
    <div class="from-group">
      <textarea name="" id="" cols="30" rows="10" class="form-input" v-model="text"></textarea>
    </div>
    <div class="form-actions">
      <button class="btn-blue">Submit</button>
    </div>
  </form>
</template>

<script>
  //
  export default {
    name: 'post-editor',

    data () {
      return {
        text: ''
      }
    },
    props: {
      threadId: {
        required: true
      }
    },
    methods: {
      save () {
        const postId = 'greatePost' + Math.random()
        const post = {
          text: this.text,
          publishedAt: Math.floor(Date.now() / 1000),
          threadId: this.threadId,
          userId: '7uVPJS9GHoftN58Z2MXCYDqmNAh2',
          '.key': postId
        }
        // console.log(this.$store.state.posts, this.thread.posts)
        this.text = ''

        this.$emit('save', {post})
      }
    }
  }
</script>

<style scoped>

</style>
