<template>
  <div class="flex-grid">

    <UserProfileCard
      v-if="!edit"
      :user="user"
      :userPostsCount="userPostsCount"
      :userThreadsCount="userThreadsCount"
    ></UserProfileCard>
    <UserProfileCardEditor
      v-if="edit"
      :user="user"
      :userPostsCount="userPostsCount"
      :userThreadsCount="userThreadsCount"
    ></UserProfileCardEditor>
    <div class="col-7 push-top">

      <div class="profile-header">
                  <span class="text-lead">
                      Joker's recent activity
                  </span>
        <a href="#">See only started threads?</a>
      </div>

      <hr>

      <PostList :posts="userPosts"></PostList>
    </div>
  </div>
</template>

<script>
  import UserProfileCard from '@/components/UserProfileCard'
  import PostList from '@/components/Postlist'
  import UserProfileCardEditor from '@/components/UserProfileCardEditor'
  import {mapGetters} from 'vuex'
  import {countObjectProperties} from '@/utils'

  export default {
    components: {
      PostList,
      UserProfileCard,
      UserProfileCardEditor
    },

    props: {
      edit: {
        type: Boolean,
        default: false
      }
    },

    computed: {
      ...mapGetters({
        user: 'authUser'
      }),

      userThreadsCount () {
        return countObjectProperties(this.user.threads)
      },

      userPostsCount () {
        return countObjectProperties(this.user.posts)
      },

      userPosts () {
        if (this.user.posts) {
          return Object.values(this.$store.state.posts)
            .filter(post => post.userId === this.user['.key'])
        }
        return []
      }
    }
  }
</script>

<style scoped>

</style>
