<!-- Not in use, was test site -->
<template>
  <div class="about">
    <h1>This is an aaaaaabout page</h1>
    <CatPictures />
    <TimerClock />
  </div>
</template>
<script>
import TimerClock from '@/components/TimerClock.vue'
import CatPictures from '@/components/CatPictures.vue'
export default {
  components: {
    TimerClock, CatPictures
  }
}
</script>
