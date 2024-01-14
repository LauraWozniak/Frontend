<template>
  <div>
    <ErinnerungenList :erinnerungen="erinnerungen" @add-erinnerung="addErinnerung" @delete-erinnerung="deleteErinnerung" />
  </div>
</template>

<script>
import ErinnerungenList from './ErinnerungenList.vue'

export default {
  components: {
    ErinnerungenList
  },
  data () {
    return {
      erinnerungen: [],
      backendBaseUrl: process.env.VUE_APP_BACKEND_BASE_URL || 'http://localhost:9090'
    }
  },
  mounted () {
    this.fetchErinnerungen()
  },
  methods: {
    fetchErinnerungen () {
      const endpoint = `${this.backendBaseUrl}/api/v1/erinnerungen`

      fetch(endpoint)
        .then(response => {
          if (!response.ok) {
            throw new Error(`Error fetching erinnerungen: ${response.statusText}`)
          }
          return response.json()
        })
        .then(result => {
          this.erinnerungen = result
        })
        .catch(error => console.error(error.message))
    },
    addErinnerung (newErinnerungText) {
      const endpoint = `${this.backendBaseUrl}/api/v1/erinnerungen`

      const requestOptions = {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({ text: newErinnerungText })
      }

      fetch(endpoint, requestOptions)
        .then(response => {
          if (!response.ok) {
            throw new Error(`Error adding erinnerung: ${response.statusText}`)
          }
          return response.json()
        })
        .then(result => {
          this.erinnerungen.push(result)
        })
        .catch(error => console.error(error.message))
    },
    deleteErinnerung (id) {
      const endpoint = `${this.backendBaseUrl}/api/v1/erinnerungen/${id}`

      const requestOptions = {
        method: 'DELETE'
      }

      fetch(endpoint, requestOptions)
        .then(response => {
          if (!response.ok) {
            throw new Error(`Error deleting erinnerung: ${response.statusText}`)
          }
        })
        .then(() => {
          this.erinnerungen = this.erinnerungen.filter(e => e.id !== id)
        })
        .catch(error => console.error(error.message))
    }
  }
}
</script>

<style scoped>

</style>
