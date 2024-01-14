<template>
  <div class="cat-container">
    <div v-if="loading">Loading...</div>
    <div v-else>
      <div class="cat-picture-box">
        <img :src="catPicture.url" alt="Cat">
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      catPicture: {},
      loading: true
    }
  },
  mounted () {
    this.fetchCatPicture()
  },
  methods: {
    async fetchCatPicture () {
      try {
        const response = await axios.get('https://api.thecatapi.com/v1/images/search')

        this.catPicture = response.data[0]
        this.loading = false
      } catch (error) {
        console.error('Error fetching cat picture:', error)
      }
    }
  }
}
</script>

<style scoped>
.cat-container {
  text-align: right; /* Align the text to the left */
  padding: 20px;
  border-radius: 20px;
  background-color: #f2f2f2;
  margin-bottom: 20px;
  max-width: 400px; /* Set a maximum width for the cat container */
  margin-left: auto;
}

.cat-picture-box {
  display: inline-block;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 100%; /* Use 100% width so it respects the max-width of the container */
}

.cat-picture-box img {
  width: 100%;
  height: auto;
}
</style>
