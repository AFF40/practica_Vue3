<template>
  <div>
    <ContactFilter @filter="filterContacts" />
    <ContactForm 
      v-if="showForm" 
      :contact="selectedContact" 
      :isEdit="isEdit" 
      @submit="handleFormSubmit" 
    />
    <button @click="addContact">Add Contact</button>
    <ContactList 
      :contacts="contacts" 
      :filteredContacts="filteredContacts"
      @edit="editContact" 
      @delete="deleteContact" 
    />
  </div>
</template>

<script>
import ContactList from '../components/ContactList.vue'
import ContactForm from '../components/ContactForm.vue'
import ContactFilter from '../components/ContactFilter.vue'

export default {
  name: 'ContactHome',
  components: {
    ContactList,
    ContactForm,
    ContactFilter
  },
  data() {
    return {
      contacts: [
        { id: 1, name: "Alice Johnson", email: "alice.johnson@example.com", address: "123 Maple Street", phone: "123-456-7890", country: "USA", city: "New York" },
        { id: 2, name: "Bob Smith", email: "bob.smith@example.com", address: "456 Oak Avenue", phone: "987-654-3210", country: "Canada", city: "Toronto" },
        { id: 3, name: "Carol White", email: "carol.white@example.com", address: "789 Pine Road", phone: "555-123-4567", country: "UK", city: "London" },
        { id: 4, name: "David Brown", email: "david.brown@example.com", address: "321 Elm Street", phone: "444-555-6666", country: "Australia", city: "Sydney" },
        { id: 5, name: "Emily Davis", email: "emily.davis@example.com", address: "654 Spruce Lane", phone: "333-444-5555", country: "USA", city: "Los Angeles" }
      ],
      filteredContacts: [],
      showForm: false,
      selectedContact: null,
      isEdit: false,
      filter: { name: '', email: '' }
    }
  },
  methods: {
    addContact() {
      this.selectedContact = { id: Date.now(), name: '', email: '', address: '', phone: '', country: '', city: '' }
      this.showForm = true
      this.isEdit = false
    },
    editContact(contact) {
      this.selectedContact = { ...contact }
      this.showForm = true
      this.isEdit = true
    },
    deleteContact(id) {
      this.contacts = this.contacts.filter(contact => contact.id !== id)
      this.filterContacts(this.filter)
    },
    handleFormSubmit(contact) {
      if (this.isEdit) {
        const index = this.contacts.findIndex(c => c.id === contact.id)
        this.contacts.splice(index, 1, contact)
      } else {
        this.contacts.push(contact)
      }
      this.showForm = false
      this.filterContacts(this.filter)
    },
    filterContacts(filter) {
      this.filteredContacts = this.contacts.filter(contact => 
        (contact.name || '').toLowerCase().includes(filter.name.toLowerCase()) && 
        (contact.email || '').toLowerCase().includes(filter.email.toLowerCase())
      )
      this.filter = filter
    }
  },
  created() {
    this.filteredContacts = this.contacts
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
  margin: 10px;
}

input {
  width: 30%;
  margin: 0 auto;
  margin-bottom: 10px;
  padding: 5px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 5px;
  display: block;
}

form {
  width: 55%;
  margin: 0 auto;
}

div {
  margin-bottom: 10px;
}

label {
  display: block;
}

table {
  width: 70%;
  border-collapse: collapse;
  margin: 0 auto;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

tr:hover {
  background-color: #f5f5f5;
}

tr {
  cursor: pointer;
}

h2 {
  text-align: center;
}

button {
  padding: 5px 10px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #00FF0D;
}

button:active {
  background-color: #4CAF50;
}

button:focus {
  outline: none;
}


</style>