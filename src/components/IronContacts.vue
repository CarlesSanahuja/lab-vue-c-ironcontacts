<template>
    <div>
      <h1>IronContacts</h1>
      <div class="Buttons">
        <!-- Botón para agregar un contacto aleatorio -->
        <button @click="addRandomContact">Add Random Contact</button>
        
        <!-- Botones para ordenar los contactos -->
        <button @click="sortByName">Sort by Name</button>
        <button @click="sortByPopularity">Sort by Popularity</button>
    </div>
     
  
      <!-- Tabla de contactos -->
      <table>
        <thead>
          <tr>
            <th>Picture</th>
            <th>Name</th>
            <th>Popularity</th>
            <th>Won Oscar</th>
            <th>Won Emmy</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="contact in displayedContacts" :key="contact.id">
            <td><img :src="contact.pictureUrl" :alt="contact.name" style="width: 50px" /></td>
            <td>{{ contact.name }}</td>
            <td>{{ contact.popularity.toFixed(2) }}</td>
            <td v-if="contact.wonOscar">🏆</td>
            <td v-else></td>
            <td v-if="contact.wonEmmy">🏆</td>
            <td v-else></td>
            <td>
              <!-- Botón para eliminar un contacto -->
              <button @click="removeContact(contact.id)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import contacts from '../contacts.json'; // Importa el archivo con los contactos
  
  export default {
    data() {
      return {
        displayedContacts: contacts.slice(0, 5), // Muestra los primeros 5 contactos
        remainingContacts: contacts.slice(5),    // El resto de los contactos
      };
    },
    methods: {
      // Función para agregar un contacto aleatorio
      addRandomContact() {
        if (this.remainingContacts.length === 0) return; // Si ya no quedan contactos, salir
  
        // Selecciona un contacto aleatorio de los restantes
        const randomIndex = Math.floor(Math.random() * this.remainingContacts.length);
        const randomContact = this.remainingContacts.splice(randomIndex, 1)[0];
  
        // Agrega el contacto seleccionado a la lista de contactos mostrados
        this.displayedContacts.push(randomContact);
      },
  
      // Función para eliminar un contacto
      removeContact(contactId) {
        // Filtra la lista de contactos mostrados para eliminar el contacto con el ID dado
        this.displayedContacts = this.displayedContacts.filter(contact => contact.id !== contactId);
      },
  
      // Función para ordenar contactos por nombre (alfabéticamente)
      sortByName() {
        this.displayedContacts.sort((a, b) => a.name.localeCompare(b.name));
      },
  
      // Función para ordenar contactos por popularidad (de mayor a menor)
      sortByPopularity() {
        this.displayedContacts.sort((a, b) => b.popularity - a.popularity);
      }
    },
  };
  </script>
   <style>
   *{
     margin: 0;
     padding: 0;
   }
   table {
     width: 100%;
     border-collapse: collapse;
     max-width: 600px;
     margin: 0 auto;
   }
   
   th, td {
     border: 1px solid #ddd;
     padding: 8px;
     text-align: center;
   }
   
   th {
     background-color: #f2f2f2;
   }
   table{
     max-width: 600px;
     margin: 0 auto;
   }
   h1{
     text-align: center;
     margin-bottom: 20px;
   }
   .Buttons{
     text-align: center;
     margin-bottom: 20px;
   }
   button{
     margin-right: 10px;
   }
   </style>
   
  