<template>
  <SearchResult :movieList = movieList />
</template>

<script>
import SearchResult from './SearchResult.vue'

export default {
  name: 'Container',
  data(){
    return{

    }
  },
  props: {
   movieList: Array
  },
  components: {
    SearchResult
  },
}
</script>

<style>

</style>