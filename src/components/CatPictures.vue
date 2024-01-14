<template>
  <div class="cat-container">
    <div v-if="!minimized">
      <div v-if="loading">Loading...</div>
      <div v-else>
        <div class="cat-picture-box">
          <img :src="catPicture.url" alt="Cat">
        </div>
      </div>
    </div>
    <button @click="toggleMinimize" class="minimize-button">{{ minimized ? '+' : '-' }}</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      catPicture: {},
      loading: true,
      minimized: false
    }
  },
  mounted () {
    this.fetchCatPicture() // Fetch initial picture

    // no new pictures if minimized
    this.intervalId = setInterval(() => {
      if (!this.minimized) {
        this.fetchCatPicture()
      }
    }, 100000)// Wie oft neue bilder(10 Sekunden)
  },
  beforeUnmount () {
    // Clear the interval when the component is destroyed
    clearInterval(this.intervalId)
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
    },
    toggleMinimize () {
      this.minimized = !this.minimized
    }
  }
}
</script>

<style scoped>
.cat-container {
  text-align: right;
  padding: 20px;
  padding-right: 40px;
  border-radius: 20px;
  background-color: #f2f2f2;
  max-width: 400px;
  position: relative;
}

.minimize-button {
  background-color: #888d82;
  color: white;
  border: none;
  border-radius: 100%;
  padding-left: 10px;
  padding-right: 10px;
  cursor: pointer;
  font-size: 18px;
  position: absolute;
  top: 5px;
  right: 5px;
  transition: background-color 0.3s ease;
  width: 30px;
}

.minimize-button:hover {
  background-color: #5b5b5b; /* Change color on hover */
}

/* Adjustments for the Font Awesome icon */
.minimize-button i {
  width: 50px;
  height: 20px;
}

.cat-picture-box {
  display: inline-block;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 100%; /* Use 100% width so it respects the max-width of the container */
  height: 100%;
}

.cat-picture-box img {
  width: 100%;
  height: 100%;
}
</style>
