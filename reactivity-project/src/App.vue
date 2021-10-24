<template>
  <div id="app">
    <h1>Scrappy</h1>
    <h2>Notes for the organized unorganized</h2>
    <h3>Add a note to get started!</h3>
    <main class="notes">
      <section class="note" v-for="note in notes" :key="note.noteId">
        <NoteComponent :style="{ backgroundColor: note.noteColor}"/> 
        <!-- <button>delete</button> -->
        <!-- @displayNewNote="addNote($event)" -->
      </section>
    </main>
    <div @mouseover="changeButton" @mouseout="changeButtonBack" class="buttons"> 
      <div v-for="color in colors" :key="color">
        <AddButton class="add-btn-component" @buttonClick="addNote" :buttonColor="color" />
      </div>
      <div>
        <button @click="getRandomColor" class="select-btn add-btn">{{ buttonStatus }}</button>
        <button @click="getRandomColor" class="select-btn mobile-btn add-btn">⇆</button>
      </div>
    </div>
  </div>
</template>

<script>
import NoteComponent from "./components/NoteComponent.vue";
import AddButton from "./components/AddButton.vue";

export default {
  name: "App",
  components: {
    NoteComponent,
    AddButton
  },
  data() {
    return {
      buttonStatus: '+',
      noteCounter: 0,
      notes: [
      ],
      colors: [
        '#FF7171', //RED
        '#FFA952', //ORANGE
        '#FFFD71', //YELLOW
        '#AAF68E', //GREEN
        '#8EE9F6', //BLUE
        '#9EC0FF', //INDIGO
        '#B48EF6', //VIOLET
        '#F4AADA', //PINK
      ], 
    }
  },
   methods: {
      addNote(color) {
        this.noteCounter++;
        const newNote = {};
        newNote['noteId'] = this.noteCounter;
        newNote['noteColor'] = color;
        this.notes.push(newNote);
      },
      changeButton() {
        this.buttonStatus = '⇆';
        document.querySelector('.select-btn').style.boxShadow = 'none';
      },
      changeButtonBack() {
        this.buttonStatus = '+';
        document.querySelector('.select-btn').style.boxShadow = '0 .75rem 1.5rem rgba(0, 0, 0, 0.25)';
      },
      getRandomColor() {
        const colorIndex = Math.floor(Math.random() * 8);
        const newNote = {};
        this.noteCounter++;
        newNote['noteId'] = this.noteCounter;
        newNote['noteColor'] = this.colors[colorIndex];
        this.notes.push(newNote);
      },
    }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Gloria+Hallelujah&display=swap');

  *, html, body {
    font-size: 62.5%;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    padding: 2%;
    font-family: 'Gloria Hallelujah', cursive;
  }
  h1, h2, h3 {
    text-align: center;
    letter-spacing: .05rem;
  }
  h1 {
    font-size: 6.5rem;
    line-height: 1.3;
  }
  h2 {
    font-size: 2rem;
  }
  h3 {
    font-size: 1.6rem;
  }
  .notes {
    overflow-y: scroll;
    padding: 5rem 2rem;
    display: grid;
    gap: 2rem;
    grid-template-columns: repeat(auto-fill, minmax(25rem, 1fr));
    justify-items: center;
  }
  .buttons {
    position: fixed;
    display: flex;
    padding: 2rem;
    bottom: 2%;
    right: 2%;
  }
  .buttons:hover {
    gap: .5rem;
  }
  .add-btn {
    /* display: none; */
    margin-left: -5rem;
    transition: all .2s;
  }
  .add-btn:hover {
    transform: translateY(-.5rem);
  }
  .select-btn {
    font-size: 3rem;
    background-color: #ececec;
    box-shadow: 0 .75rem 1.5rem rgba(0, 0, 0, 0.25);
  }
  .mobile-btn {
    display: none;
    box-shadow: none;
  }
  .buttons:hover .add-btn {
    margin: 0;
    /* display: block; */
  }

  @media only screen and (max-width: 768px) {
    .buttons {
      overflow-y: scroll;
      flex-direction: column;
      gap: 0;
      right: 0;
      bottom: 0;
    }
    .buttons:hover {
      gap: 0;
    }
    .add-btn {
      margin-left: 0;
      width: 3.5rem;
      height: 3.5rem;
    }
    .add-btn:hover {
      transform: none;
    }
    .select-btn {
      display: none;
    }
    .mobile-btn {
      display: block;
      font-size: 2rem;
    }
 } 
  
</style>
