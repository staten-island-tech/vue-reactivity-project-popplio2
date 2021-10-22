<template>
    <div class="note-container">
      <div class="note-header">
        <button class="copy-btn" @click="copyNote">CTC</button>
        
        <button class="delete-btn" @click="deleteNote">X</button>
      </div>
      <textarea class="note-text" placeholder="Write in me!"></textarea>
    </div>
</template>

<script>
export default {
  data() {
    return {
      colors: [
        '#FF7171', //RED
        '#FFAA68', //ORANGE
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
    deleteNote(event) {
      event.target.parentNode.parentNode.parentNode.remove();
    },
    copyNote(event) {
      navigator.clipboard.writeText(event.target.parentNode.nextSibling.value);
    }
  }
};
</script>

<style>
  .note-container {
    width: 25rem;
    height: 25rem;
    box-shadow: 0 .5rem 1.5rem rgba(0, 0, 0, 0.2);
    transition: all .3s;
  }
  .note-container:hover {
    transform: scale(1.1);
    z-index: 1;
  }
  .note-header {
    display: flex;
    justify-content: space-between;
    width: 25rem;
    height: 4rem;
    padding: 0 1.5rem;
    background-color: rgba(0, 0, 0, 0.05);
  }
  .delete-btn {
    font-family: 'Gloria Hallelujah', cursive;
    font-size: 2rem;
    color: rgb(156, 0, 0);
    border: none;
    background-color: transparent;
    cursor: pointer;
  }
  .note-text {
    display: inline-block;
    font-family: 'Gloria Hallelujah', cursive;
    font-size: 1.6rem;
    letter-spacing: .05rem;
    line-height: 1.4;
    width: 25rem;
    height: 20.5rem;
    padding: 1rem 1.5rem;
    background-color: transparent;
    border: none;
    resize: none;
    outline: none;
  }
  .note-text::placeholder {
    color: #000;
  }
  .note-text:focus::placeholder {
    color: transparent;
  }
</style>