<template>
  <h1>Deine Erinnerungen</h1>
  <div class="erinnerung">
    <div class="row row-cols-1 row-cols-md-4 g-4">
      <div class="col" v-for="erinnerung in erinnerungen" :key="erinnerung.id">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title">{{ erinnerung.id }}</h5>
            <p class="card-text">
              {{ erinnerung.text }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ErinnerungenView',
  data () {
    return {
      erinnerungen: []
    }
  },
  mounted () {
    const backendBaseUrl = process.env.VUE_APP_BACKEND_BASE_URL || 'http://localhost:9090'
    console.log('backendBaseUrl:', backendBaseUrl)
    const endpoint = `${backendBaseUrl}/api/v1/erinnerungen`

    const requestOptions = {
      method: 'GET',
      redirect: 'follow'
    }

    fetch(endpoint, requestOptions)
      .then(response => response.json())
      .then(result => result.forEach(erinnerung => {
        this.erinnerungen.push(erinnerung)
      }))
      .catch(error => console.log('error', error))
  }
}
</script>

<style scoped>

</style>
