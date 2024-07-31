<template>
    <div>
      <h2>{{ isEdit ? 'Edit' : 'Add' }} Contact</h2>
      <form @submit.prevent="submitForm">
        <div>
          <label>Name:</label>
          <input v-model="localContact.name" required />
        </div>
        <div>
          <label>Email:</label>
          <input v-model="localContact.email" type="email" required />
        </div>
        <div>
          <label>Address:</label>
          <input v-model="localContact.address" required />
        </div>
        <div>
          <label>Phone:</label>
          <input v-model="localContact.phone" required />
        </div>
        <div>
          <label>Country:</label>
          <input v-model="localContact.country" required />
        </div>
        <div>
          <label>City:</label>
          <input v-model="localContact.city" required />
        </div>
        <button type="submit">{{ isEdit ? 'Update' : 'Actualizar' }} Contact</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: ['contact', 'isEdit'],
    data() {
      return {
        localContact: { ...this.contact }
      }
    },
    watch: {
      contact: {
        handler(newVal) {
          this.localContact = { ...newVal }
        },
        deep: true
      }
    },
    methods: {
      submitForm() {
        this.$emit('submit', this.localContact)
      }
    }
  }
  </script>
  
    