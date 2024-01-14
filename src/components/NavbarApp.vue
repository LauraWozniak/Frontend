<template>
  <nav class="navbar navbar-expand-lg navbar-dark gradient-custom">
    <div class="container-fluid">
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav"
              aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav me-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/erinnerungen" style="font-size: 40px; font-weight: bold; margin-left: 50px;" active-class="active-link">Erinnerungen</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
<script>
export default {
  name: 'NavbarApp'
}
</script>

<style scoped>
.gradient-custom {
  background: #342948;
  background: -webkit-linear-gradient(to right, rgb(9, 11, 38), rgb(58, 24, 117));
  background: linear-gradient(to right, rgb(64, 56, 77), rgb(62, 55, 126));
}
.navbar-brand {
  font-size: 1.5em;
}
.nav-link {
  font-size: 1.2em;
}
.active-link {
  color: #daded4;
}
</style>
