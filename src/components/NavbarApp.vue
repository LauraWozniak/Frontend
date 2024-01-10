<template>
  <nav class="navbar navbar-expand-lg navbar-dark gradient-custom">
    <div class="container-fluid">
      <!-- Adjusted alignment for "Navbar" text -->
      <router-link class="navbar-brand me-auto" to="/">
        <div>
          <i class="material-icons">Info</i>
        </div>
        Remindr
      </router-link>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav"
              aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav me-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/" style="font-size: 30px; font-weight: bold; margin-right: 50px; margin-left: 90px;">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about" style="font-size: 30px; font-weight: bold; margin-right: 50px;">About</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/erinnerungen" style="font-size: 30px; font-weight: bold; margin-right: 50px;">Erinnerungen</router-link>
          </li>
        </ul>

        <!-- "Settings" link with ms-auto class for right alignment -->
        <ul class="navbar-nav ms-auto ">
          <li class="nav-item me-1 me-lg-0">
            <a class="nav-link" href="#">
              <div>
              <i class="material-icons" style="font-size: 2.1em;">settings</i>
              </div>
              Settings
            </a>
          </li>
          <li class="nav-item me-3 me-lg-0">
            <a class="nav-link" href="#">
              <div>
              <i class="material-icons" style="font-size: 2.1em;">light_mode</i>
              </div>
              Mode
            </a>
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
  background: #3a7928;
  background: -webkit-linear-gradient(to right, rgb(113, 241, 245), rgb(113, 250, 177));
  background: linear-gradient(to right, rgb(89, 159, 130), rgb(88, 124, 59));
}
.navbar-brand {
  font-size: 1.5em; /* Adjust the font size as needed */
}
.nav-link {
  font-size: 1.2em; /* Adjust the font size as needed */
}
</style>
