<script>
  export default {
    data() {
      return {

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
        <textarea class="form-control" aria-label="With textarea"></textarea>
      </div>
    </div>

  </nav>

</div>
</template>