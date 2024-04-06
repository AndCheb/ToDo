<script>
  const LS_KEY = 'toDo';
  export default {
    data() {
      return {
        cards: JSON.parse(localStorage.getItem(LS_KEY) || '[]'),
        noteId: 1,
        noteText: '',

        allClass: 'btn-success',
        activeClass: 'btn-light',
        completedClass: 'btn-light',
      }
    },

    methods: {
      resetButtonStyle() {
        this.cards.forEach((i) => {
          i.hide = false;
        });
        this.allClass = 'btn-light';
        this.activeClass = 'btn-light';
        this.completedClass = 'btn-light';
      },

      addNote() {
        this.showActive()
        if (this.noteText.trim().length)
        this.cards.push({
          id: this.noteId++,
          title: new Date().toLocaleString(),
          text: this.noteText,
          actual: true,
          hide: false,
        });
        this.noteText = '';
      },

      checkNote(i) {
        this.showActive();
        this.cards[i].actual = false;
        this.cards[i].hide = true;
      },

      removeNote(index) {
        this.cards.splice(index, 1);
      },

      showAll() {
        this.resetButtonStyle();
        this.allClass = 'btn-success';
      },

      showActive() {
        this.resetButtonStyle();
        this.cards.forEach((i) => {
          if (!i.actual) {
            i.hide = true;
          }
        });
        this.activeClass = 'btn-success';
      },

      showCompleted() {
        this.resetButtonStyle();
        this.cards.forEach((i) => {
          if (i.actual) {
            i.hide = true;
          }
        });
        this.completedClass = 'btn-success';
      },

      clearCompleted() {
        this.cards = this.cards.filter((i) => i.actual !== false);
      }
    },

    watch: {
      cards: {
        handler(cards) {
          localStorage.setItem(LS_KEY, JSON.stringify(cards))
        },
        deep: true,
      }
    },
  }
</script>
  
<template>
<div class="wrapper" data-bs-theme="dark">

  <nav class="navbar bg-body-tertiary">
    
    <div class="container-fluid">
      <span class="navbar-brand mb-0 h1">Create a new task!</span>

      <div class="buttons-wrapper" role="group">
        <button 
          type="button" 
          :class="allClass"
          class="btn" 
          @click="showAll"
        >
          All
        </button>
        <button 
          type="button" 
          class="btn" 
          :class="activeClass" 
          @click="showActive"
        >
          Active
        </button>
        <button 
          type="button" 
          class="btn" 
          :class="completedClass"
          @click="showCompleted"
        >
          Completed
        </button>
      </div>

      <button 
        type="button"
        class="btn btn-warning"
        @click="clearCompleted"
      >
        Clear completed
      </button>

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
    <div 
      class="card mb-3"
      v-for="(card, index) in cards"
      :key="card.id"
      v-show="!card.hide"
    >
      <div class="card-body">
        <h5 class="card-title">{{ card.title }}</h5>
        <hr>
        <p class="card-text mb-4">{{ card.text }}</p>
        <hr>
        <div class="card-buttons">
          <button 
            type="button" 
            class="btn btn-success" 
            @click="checkNote(index)" 
            v-show="card.actual"
          >
            Complete
          </button>
          <button type="button" class="btn btn-danger" @click="removeNote(index)">Remove</button>
          <button type="button" class="btn btn-secondary">Edit</button>
        </div>
      </div>
    </div>
  </div>

</div>
</template>