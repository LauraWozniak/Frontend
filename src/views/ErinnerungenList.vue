<!-- src/components/ErinnerungenList.vue -->
<template>
  <div class="main-container">
    <!-- Timer -->
    <div class="timer-container">
      <TimerClock />
    </div>
    <!-- erinnerungsliste -->
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
    <!-- katzenbilder -->
    <div class="cat-pictures">
      <CatPictures />
    </div>
  </div>
</template>
<script>
import TimerClock from '@/components/TimerClock.vue'
import CatPictures from '@/components/CatPictures.vue'

export default {
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
    }
  }
}
</script>
<style scoped>
.main-container {/* do not touch the single containers*/
  display: flex;
}

.timer-container {
  flex: 1;
}
.cat-pictures {
  flex: 1;
  max-width: 400px;
  max-height: 400px;
  margin-left: 20px;
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
.modern-button {
  background-color: #888d82;
  color: white;
  border: none;
  border-radius: 20px;
  padding: 10px 20px;
  cursor: pointer;
}
</style>
