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
      contacts: [],
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
        (contact.name || '').includes(filter.name) && 
        (contact.email || '').includes(filter.email)
      )
      this.filter = filter
    }
  },
  created() {
    this.filteredContacts = this.contacts
  }
}
</script>
