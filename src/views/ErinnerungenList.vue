<!-- src/components/ErinnerungenList.vue -->
<template>
  <div class="main-container">
    <div class="timer-container">
      <TimerClock />
    </div>
  <div class="erinnerungen-list" style="margin-top: 40px;">
    <div class="list-container">
      <div v-for="erinnerung in erinnerungen" :key="erinnerung.id" class="erinnerung-item">
        <div class="erinnerung-details">
          <div class="erinnerung-text">{{ erinnerung.text }}</div>
        </div>
        <button class="erinnerung-done" @click="deleteErinnerung(erinnerung.id)"></button>
      </div>
    <!-- input feld für neue erinnerung -->
    <div class="new-erinnerung">
      <input class= "modern-input"  v-model="newErinnerungText" placeholder="Neuer Eintrag"/>
      <button class ="modern-button" @click="addErinnerung">Add</button>
    </div>
  </div>
  </div>
    <div class="cat-pictures">
      <CatPictures />
    </div>
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
.main-container {
  display: flex;
}

.timer-container {
  flex: 1; /* Takes 1/3 of the available width */
}
.cat-pictures {
  flex: 1; /* Takes 1/3 of the available width */
  max-width: 400px; /* Optional: Set a maximum width for the cat pictures */
  max-height: 400px;
  margin-left: 20px; /* Adjust the margin between list and cat pictures */
}
.cat-pictures {
  position: absolute;
  top: 130px;
  right: 20px;
}

.modern-button {
  background-color: #888d82;
  color: white;
  border: none;
  border-radius: 20px;
  padding: 10px 20px;
  cursor: pointer;
  margin: 5px;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

.modern-button:hover {
  background-color: #5b5b5b;
  transform: scale(1.1);
}

.erinnerungen-list {
  position: absolute;
  top: 260px;
  left: 20px;
  max-width: 400px;
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
  padding-right: 10px;
}

.erinnerung-details {
  display: flex;
  align-items: center;
}

.erinnerung-text {
  flex-grow: 1;
  padding-right: 10px;
}

.erinnerung-done {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background-color: #5b5b5b;
  border: none;
  cursor: pointer;
  transition: transform 0.3s ease, background-color 0.3s ease;
}

.erinnerung-done:hover {
  transform: scale(1.2);
  background-color: #79b046;
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
  outline: none;
  background-color: #f2f2f2;
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
  padding: 10px 20px;
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
</style>
