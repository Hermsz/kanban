<template>
    <v-dialog max-width="600px">
    <v-btn flat slot="activator" class="success" >Add new Task</v-btn>
    <v-card>
      <v-card-title>
        <h2>Add a new Product</h2>
      </v-card-title>
      <v-form class="px-3">
        <v-text-field label="Title" v-model="title"></v-text-field>
        <v-text-field label="Description" v-model="description"></v-text-field>
        <v-text-field label="Point" v-model="point"></v-text-field>
        <v-text-field label="Assigned To" v-model="assignedTo"></v-text-field>
        <v-btn flat class="success mx-0 mt-3" @click="addTask">Submit</v-btn>
      </v-form>
    </v-card>
  </v-dialog>
</template>

<script>
  import db from '@/firebase.js'

export default {
  data() {
    return {
      title: '',
      description: '',
      point: '',
      assignedTo: '',
      items: ['BackLog', 'ToDo', 'OnGoing', 'Finished']
    }
  },
  methods: {
    addTask() {
      db.collection('todos').add({
        title: this.title,
        description: this.description,
        point: this.point,
        assignedTo: this.assignedTo,
        status: 'BackLog'
      })
      .then((doc) => {
        console.log(`Document written with ID`, doc.id)
      })
      .catch(err => {
        console.log(`Error adding document`, err)
      })

    }
  }
}
</script>

<style>

</style>
