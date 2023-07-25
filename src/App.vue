<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model="note"></textarea>
        <button class="add-btn" @click="addNote">Add Note</button>
        <button class="close-btn" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Zosar Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <h3>Let's Add Some Notes To Remember ..</h3>
      <div class="note-cards">
        <div
          class="note-card"
          v-for="note of notes"
          :key="note.id"
          :style="{ backgroundColor: note.backgroundColor }"
        >
          <p class="note-text">{{ note.text }}</p>
          <p class="note-date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import { ref } from "vue";
export default {
  name: "App",
  setup() {
    const showModal = ref(false);
    const note = ref("");
    const notes = ref([]);
    function getRandomColor() {
      return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
    }

    const addNote = () => {
      if (note.value) {
        notes.value.push({
          id: Math.floor(Math.random() * 10000),
          text: note.value,
          date: new Date().toLocaleDateString("en-US"),
          backgroundColor: getRandomColor(),
        });
        note.value = "";
        showModal.value = false;
      }
    };
    return {
      showModal,
      note,
      notes,
      addNote,
    };
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
main {
  height: 100vh;
}
.container {
  max-width: 1000px;
  padding: 12px;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
.note-cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
h1 {
  font-size: 3rem;
  font-weight: bold;
}
button {
  width: 50px;
  height: 50px;
  background-color: rgb(15, 10, 10);
  color: white;
  border-radius: 100%;
  border: none;
  cursor: pointer;
  font-size: 1.5rem;
}
.note-card {
  width: 240px;
  height: 240px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.note-text {
  line-height: 1.25;
  font-size: 17.5px;
  font-weight: bold;
  word-wrap: break-word;
}
.note-date {
  font-size: 12.5px;
  margin-top: auto;
}
.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  transform: translate(-50%, -50%);
  top: 50%;
  left: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}
h3 {
  color: rgb(67, 11, 11);
  font-size: 1.5rem;
  padding-bottom: 15px;
}
.modal {
  width: 750px;
  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}

.add-btn {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}
.close-btn {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: rgb(255, 7, 7);
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}
.modal p {
  margin-left: auto;
  font-size: 20px;
  z-index: 100000;
  cursor: pointer;
}

textarea {
  width: 100%;
  height: 200px;
  padding: 5px;
  font-size: 20px;
}
</style>
