<!-- src/components/ErinnerungenList.vue -->
<template>
  <div class="erinnerungen-list">
    <div class="erinnerungen-box">
      <div v-for="erinnerung in erinnerungen" :key="erinnerung.id" class="erinnerung-item">
        <div class="erinnerung-details">
          <div class="erinnerung-checkbox" @click="toggleErinnerung(erinnerung)">
            <div v-if="erinnerung.completed" class="checkbox-checked">&#10003;</div>
            <div v-else class="checkbox-unchecked"></div>
          </div>
          <div class="erinnerung-text">{{ erinnerung.text }}</div>
        </div>
        <button class="erinnerung-delete" @click="deleteErinnerung(erinnerung.id)">Delete</button>
      </div>
    </div>

    <!-- Add new erinnerung input and button -->
    <div class="new-erinnerung">
      <input v-model="newErinnerungText" placeholder="New Erinnerung" />
      <button @click="addErinnerung">Add</button>
    </div>
  </div>
</template>

<script>
export default {
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
  align-items: center;
}

.erinnerungen-box {
  width: 300px;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 15px;
  margin-bottom: 20px;
}

.erinnerung-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}

.erinnerung-details {
  display: flex;
  align-items: center;
}

.erinnerung-checkbox {
  width: 20px;
  height: 20px;
  border: 1px solid #ccc;
  border-radius: 4px;
  cursor: pointer;
  margin-right: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
}

.checkbox-checked {
  color: green;
}

.checkbox-unchecked {
  width: 100%;
  height: 100%;
  background-color: white;
}

.erinnerung-text {
  flex-grow: 1;
}

.erinnerung-delete {
  background-color: #dc3545;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}
</style>
