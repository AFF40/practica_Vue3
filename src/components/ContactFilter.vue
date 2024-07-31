<template>
    <div>
      <input 
        id="name"
        type="text" 
        placeholder="Filtrar por nombre" 
        v-model="filter.name"
        @input="onInput" 
      />
      <input 
        id="email"
        type="text" 
        placeholder="Filtrar por email" 
        v-model="filter.email"
        @input="onInput" 
      />
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        filter: { name: '', email: '' }
      }
    },
    methods: {
      onInput() {
        this.$emit('filter', this.filter)
      }
    }
  }
  </script>
  
   