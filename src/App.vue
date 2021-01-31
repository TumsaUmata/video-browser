<template>
  <div class="container">
      <SearchBar @termChange="onTermChange"></SearchBar>
      <video-list :videos="videos"></video-list>
  </div>
</template>

<script>
import axios from 'axios'
import SearchBar from './components/SearchBar'
import VideoList from './components/VideoList'

const API_KEY = 'AIzaSyBuwR-49mgCVHvUt6M6UcijnimjBLtXpVk'

export default {
    name: 'App',
    components: {
      SearchBar,
      VideoList
    },
    data() {
      return {
        videos: []
      }
    },
    methods: {
      onTermChange(searchTerm){
        axios.get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm
          }
        }).then(response => {
          this.videos = response.data.items
        })
      }
    }
}
</script>

<style>

</style>