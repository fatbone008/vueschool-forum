<template>

  <div class="forum-list">

    <h2 class="list-title">
      <router-link :to="{name: 'Category', params:{id:category['.key']} }">{{category.name}}</router-link>
    </h2>

    <ForumList :forums="categoryForums"></ForumList>
  </div>
</template>

<script>
  import ForumList from './ForumList'
  import sourceData from '@/data'

  export default {
    name: 'CategoryListItem',
    components: {
      ForumList
    },
    props: {
      category: {
        required: true,
        type: Object
      }
    },
    computed: {
      categoryForums () {
        // console.log('sourceData.forums:', sourceData.forums)
        return Object.values(sourceData.forums)
          .filter(forum => forum.categoryId === this.category['.key'])
      }
    }
  }
</script>

<style scoped>

</style>
