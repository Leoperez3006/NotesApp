<script setup>
import {ref} from "vue";

const showModal = ref(false);

const newTitle = ref("");
const newNote = ref("");

const notes = ref([]);

const addNote = () => {
  notes.value.push({
    id: Math.floor(Math.random() * 12345),
    title: newTitle.value,
    note: newNote.value,
    date: new Date(),

  });
  showModal.value = false;
  newTitle.value = "";
  newNote.value= "";

}

</script>
<template>
  <main>
    <div v-show="showModal"  class="overlay">
      <div class="modal">
        <textarea v-model="newTitle" name="Title" id="title" placeholder="Title" cols="20" rows="1" class="title"></textarea>
        <textarea v-model="newNote" name="note" id="note"   placeholder="Insert your text here..." cols="30" rows="10"></textarea>
        <button @click="addNote()" class="add"> Add</button>
        <button @click="showModal=false" class="cancel">cancel</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Sticky Notes</h1>
        <button @click="showModal=true">Add a note</button>
      </header>
      <div class="card-container">
        <div v-for="note in notes" class="card">
          <p class="title">{{ note.title }}</p>
          <p class="main-text">{{ note.note }}.</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>

      </div>
    </div>
  </main>
</template>

<style scoped>
main{

  height: 100vh;
  width: 100vw;
  background-color: rgb(30, 30, 32);
}

.container{

  margin: 0 auto;
}
header{
  color: rgb(163, 185, 211);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  padding-left: 10%;
  padding-right: 10%;
  background-color: rgb(23, 23, 26);
}
h1{
  font-weight: bolder;
  font-size: 50px;
}
header button{
  padding: 2%;
  background-color: rgb(163, 185, 211);
  cursor: pointer;
  font-weight: bold;
  border-radius: 5%;
}

.card-container{
  margin: 20px;
  display: flex;
  flex-wrap: wrap;
}
.card{
  width: 250px;
  height: 250px;
  background-color: azure;
  padding: 15px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 15px;
}
.title{
  font-weight: bold;
  font-size: 25px;
}
.date{
  font-weight: lighter;
  font-size: 12px;
}

.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.726);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
} 
.modal{
  width: 750px;
  background-color: rgba(58, 58, 58, 0.911);
  border-radius: 10px;
  padding: 25px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.add{
  padding: 5px;
  margin-top: 5px;
  cursor: pointer;
  background-color: rgb(163, 185, 211);
  color: rgb(230, 230, 230);  
  border: none;
}
.cancel{
  padding: 5px;
  margin-top: 5px;
  cursor: pointer;
  background-color: rgba(201, 0, 0, 0.733);
  color: rgb(230, 230, 230);
  border: none;
}

</style>

