<template>
  <div id="app">

    <h1>Scrappy</h1>
    <h2>Notes for the organized unorganized</h2>

    <div class="dropdown">
      <h3 @click="dropdownClick" v-if="!isDropdown" class="theme-header">Themes</h3>
      <button @click="dropdownClick" v-else class="theme-close">X</button>
      <transition name="slide-fade">
        <div class="dropdown-options" v-if="isDropdown">
          <button @click="toNoTheme" class="theme-btn">Vanilla</button>
          <button @click="toCoolTheme" class="theme-btn">Cool</button>
          <button @click="toWarmTheme" class="theme-btn">Warm</button>   
          <button @click="toRainbowTheme" class="theme-btn">Rainbow</button>
          <button @click="toPastelTheme" class="theme-btn">Pastel</button>
        </div>
     </transition>
    </div>

    <main class="notes">
      <section class="note" v-for="note in notes" :key="note.noteId">
        <NoteComponent :style="{ backgroundColor: note.noteColor }"/> 
        <!-- <button>delete</button> -->
        <!-- @displayNewNote="addNote($event)" -->
      </section>
    </main>

    <div @mouseover="changeButton" @mouseout="changeButtonBack" class="buttons"> 
      <div v-for="color in colors" :key="color.name">
        <AddButton class="add-btn-component" @buttonClick="addNote" :buttonColor="color.code" :aria-label="color.name"/>
      </div>
      <div>
        <button @click="getRandomColor" class="select-btn add-btn">{{ buttonStatus }}</button>
        <button @click="getRandomColor" class="select-btn mobile-btn add-btn">?</button>
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
      isDropdown: false,
      noteCounter: 0,
      notes: [
        {
          noteId: 0,
          noteColor: '#FFFD71'
        }
      ],
      colors: [
        {
          name: 'red',
          code: '#FF7171',
        },
        {
          name: 'orange',
          code: '#FFA952',
        },
        {
          name: 'yellow',
          code: '#FFFD71',
        },
        {
          name: 'green',
          code: '#AAF68E',
        },
        {
          name: 'blue',
          code: '#8EE9F6',
        },
        {
          name: 'indigo',
          code: '#9EC0FF',
        },
        {
          name: 'violet',
          code: '#B48EF6',
        },
        {
          name: 'pink',
          code: '#F4AADA',
        },
      ], 
    }
  },
  mounted() {
    //credits to andrew boodman on quora
    let lastScrollHeight = 0; 
    function autoScroll() { 
      const sh = document.documentElement.scrollHeight; 
      if (sh != lastScrollHeight) { 
        lastScrollHeight = sh; 
        document.documentElement.scrollTop = sh; 
      } 
    } 
    window.setInterval(autoScroll, 100); 
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
        this.buttonStatus = '?'; //⇆
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
        newNote['noteColor'] = this.colors[colorIndex].code;
        this.notes.push(newNote);
      },
      toNoTheme() {
        document.documentElement.setAttribute('theme', 'none');
      },
      toCoolTheme() {
        document.documentElement.setAttribute('theme', 'cool');
      },
      toWarmTheme() {
        document.documentElement.setAttribute('theme', 'warm');
      },
      toRainbowTheme() {
        document.documentElement.setAttribute('theme', 'rainbow');
      },
      toPastelTheme() {
        document.documentElement.setAttribute('theme', 'pastel');
      },
      dropdownClick() {
        if(!this.isDropdown) {
          this.isDropdown = true;
          document.querySelector('.dropdown').style.textAlign = 'right';
        } else {
          this.isDropdown = false;
          document.querySelector('.dropdown').style.textAlign = 'center';
        }
      }
    }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Gloria+Hallelujah&display=swap');

  :root {
    --box-shadow: 0 .5rem 1.5rem rgba(0, 0, 0, 0.2);
  }
  :root[theme="none"] {
    --gradient: none;
  }
  :root[theme="cool"] {
    --gradient: linear-gradient(to right top, #ff7171, #fb81b9, #d5a0ee, #a2bdff, #85d3ff, #89d7ff, #8ddaff, #91deff, #a1d4ff, #bdc7ff, #dcb8f4, #f4aada);
  }
  :root[theme="warm"] {
    --gradient: linear-gradient(to right top, #ff7171, #ff8a5d, #f9a550, #e9bf4f, #d2d860, #ddd965, #e7d96b, #f1da71, #ffc47e, #ffb29c, #ffa9be, #f4aada);
  }
  :root[theme="rainbow"] {
    --gradient: linear-gradient(to right top, #ff7171, #ffa952, #f4b94f, #e7c953, #d7d75e, #c5e56f, #99eb89, #67eea9, #00eecb, #00e0f8, #00ccff, #53b1ff, #b48ef6);
  }
  :root[theme="pastel"] {
    --gradient:  
      radial-gradient(at 40% 20%, hsla(28,100%,74%,1) 0, transparent 50%),  
      radial-gradient(at 80% 0%, hsla(189,100%,56%,1) 0, transparent 50%),  
      radial-gradient(at 0% 50%, hsla(355,85%,93%,1) 0, transparent 50%),  
      radial-gradient(at 80% 50%, hsla(340,100%,76%,1) 0, transparent 50%),  
      radial-gradient(at 0% 100%, hsla(22,100%,77%,1) 0, transparent 50%),  
      radial-gradient(at 80% 100%, hsla(242,100%,70%,1) 0, transparent 50%),  
      radial-gradient(at 0% 0%, hsla(343,100%,76%,1) 0, transparent 50%);
  }

  *, html, body {
    font-size: 62.5%;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  html {
    scroll-behavior: smooth;
    min-height: 100%; 
    /* so that gradient stretches to bottom of page without repeating */
  }
  body {
    padding: 2%;
    font-family: 'Gloria Hallelujah', cursive;
    background-image: var(--gradient);
  }
  h1, h2 {
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
  .dropdown {
    position: fixed;
    top: 2%;
    right: 2%;
    text-align: center;
    background-color: #ececec;
    padding: 1rem 1.5rem;
    border: .1rem solid;
    border-radius: 3rem;
    transition: all .3s;
    z-index: 1;
  }
  .dropdown:hover {
    transform: translateY(-.5rem);
    box-shadow: var(--box-shadow);
  }
  .dropdown h3,
  .dropdown button {
    font-size: 1.6rem;
    cursor: pointer;
  }
  .dropdown button {
    font-family: 'Gloria Hallelujah', cursive;
    border: none;
  }
  .dropdown .theme-close {
    font-size: 2rem;
  }

  .slide-fade-enter-active {
    transition: all .3s ease;
  }
  .slide-fade-enter, .slide-fade-leave-to {
    transform: translateY(-1rem);
    opacity: 0;
  }
  .dropdown-options {
    display: flex;
    flex-direction: column;
  }
  .theme-btn {
    font-size: 1.6rem;
    padding: 1rem 1.5rem;
    cursor: pointer;
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
    box-shadow: var(--box-shadow);
  }
  .mobile-btn {
    display: none;
    box-shadow: none;
  }
  .buttons:hover .add-btn {
    margin: 0;
  }

  @media only screen and (max-width: 1200px) {
    .dropdown:hover {
      transform: none;
      box-shadow: none;
    }
    .buttons {
      gap: 0;
      right: 0;
      bottom: 0;
    }
    .buttons {
      gap: .5rem;
    }
    .buttons:hover {
      gap: .5rem;
    }
    .add-btn {
      margin-left: 0;
      width: 4.5rem;
      height: 4.5rem;
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
  @media only screen and (max-width: 768px) {
    .dropdown {
      bottom: 2%;
      left: 2%;
      top: unset;
      right: unset;
      padding: 1rem;
    }
    .dropdown h3 {
      font-size: 1.5rem;
    }
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
