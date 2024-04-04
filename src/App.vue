<script>

  export default {
    data() {
      return {
        noteId: 1,
        noteText: '',
        cards: [
          {
            id: 0,
            title: new Date().toLocaleString(),
            text: 'some text lorem',
          },
        ]
      }
    },

    methods: {
      addNote() {
        if (this.noteText.trim().length)
        this.cards.push({
          id: this.noteId++,
          title: new Date().toLocaleString(),
          text: this.noteText,
        });
        this.noteText = '';
      }
    }
  }
</script>
  
<template>
<div class="wrapper" data-bs-theme="dark">

  <nav class="navbar bg-body-tertiary">
    
    <div class="container-fluid">
      <span class="navbar-brand mb-0 h1">Create a new task!</span>

      <div class="buttons-wrapper" role="group">
        <button type="button" class="btn btn-light">All</button>
        <button type="button" class="btn btn-primary">Active</button>
        <button type="button" class="btn btn-success">Completed</button>
      </div>

      <button type="button" class="btn btn-warning" disabled>Clear completed</button>

      <div class="input-group">
        <span class="input-group-text">To do:</span>
        <textarea 
          class="form-control" 
          aria-label="With textarea" 
          
          maxlength="250"
          value=""
          v-model="noteText"
        >
        </textarea>
        <button type="button" class="btn btn-info" @click="addNote">Add</button>
      </div>
    </div>

  </nav>

  <div class="cards">
    <div class="card mb-3"  v-for="card in cards" :key="card.id">
      <div class="card-body">
        <h5 class="card-title">{{ card.title }}</h5>
        <hr>
        <p class="card-text mb-4">{{ card.text }}</p>
        <hr>
        <div class="card-buttons">
          <button type="button" class="btn btn-success">Complete</button>
          <button type="button" class="btn btn-danger">Remove</button>
          <button type="button" class="btn btn-secondary">Edit</button>
        </div>
      </div>
    </div>
  </div>

</div>
</template>