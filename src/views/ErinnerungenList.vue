<!-- src/components/ErinnerungenList.vue -->
<template>
  <TimerClock />
  <div class="erinnerungen-list" style="margin-top: 40px;">
    <div class="list-container">
      <div v-for="erinnerung in erinnerungen" :key="erinnerung.id" class="erinnerung-item">
        <div class="erinnerung-details">
          <!-- Removed the checkbox section -->
          <div class="erinnerung-text">{{ erinnerung.text }}</div>
        </div>
        <button class="erinnerung-done" @click="deleteErinnerung(erinnerung.id)"></button>
      </div>
    <!-- Add new erinnerung input and button -->
    <div class="new-erinnerung">
      <input class= "modern-input"  v-model="newErinnerungText" placeholder="Neuer Eintrag"/>
      <button class ="modern-button" @click="addErinnerung">Add</button>
    </div>
  </div>
  </div>
  <div class="cat-container">
    <CatPictures />
  </div>
</template>
<script>
import TimerClock from '@/components/TimerClock.vue'
import CatPictures from '@/components/CatPictures.vue'

export default {
  // eslint-disable-next-line vue/no-unused-components
  components: { CatPictures, TimerClock },
  props: {
    erinnerungen: Array
  },
  data () {
    return {
      newErinnerungText: ''
    }
  },
  methods: {
    addErinnerung () {
      if (this.newErinnerungText.trim() !== '') {
        this.$emit('add-erinnerung', this.newErinnerungText.trim())
        this.newErinnerungText = ''
      }
    },
    deleteErinnerung (id) {
      this.$emit('delete-erinnerung', id)
    },
    toggleErinnerung (erinnerung) {
      this.$emit('toggle-erinnerung', erinnerung.id)
    }
  }
}
</script>
<style scoped>
/* Add styling as needed */
.erinnerungen-list {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding-left: 20px;
  padding-top: 50px;
}

.list-container {
  width: 100%;
  max-width: 400px;
  background-color: #f2f2f2;
  border-radius: 20px;
  padding: 15px;
  margin-bottom: 20px;
}

.erinnerung-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding-right: 10px; /* Add padding to the right of each item */
}

.erinnerung-details {
  display: flex;
  align-items: center;
}

.erinnerung-text {
  flex-grow: 1;
  padding-right: 10px; /* Add padding to the right of the text */
}

.erinnerung-done {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background-color: #5b5b5b;
  border: none;
  cursor: pointer;
  transition: transform 0.3s ease, background-color 0.3s ease; /* Add transition effect for color change */
}

/* Add hover effect for the button */
.erinnerung-done:hover {
  transform: scale(1.2); /* Scale up on hover */
  background-color: #79b046; /* Change color on hover */
}

.new-erinnerung {
  margin-top: 20px;
  display: flex;
  align-items: center;
}
.modern-input {
  flex-grow: 1;
  border: none;
  border-radius: 20px;
  padding: 10px;
  margin-right: 10px;
  outline: none; /* Remove the outline */
  background-color: #f2f2f2; /* Background color */
}

.input-field {
  flex-grow: 1;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 10px;
  margin-right: 10px;
}

.modern-button {
  background-color: #888d82;
  color: white;
  border: none;
  border-radius: 20px;
  padding: 10px 20px; /* Adjust padding for a rounder button */
  cursor: pointer;
}
.add-button {
  background-color: #3b4a57;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 4px;
  cursor: pointer;
}
.cat-container{
  display: flex;
  justify-content: space-between;
  align-items: flex-start; /* Align to the top */
  padding-right: 20px;
}
</style>
