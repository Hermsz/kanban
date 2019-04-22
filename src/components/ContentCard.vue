<template>
  <div class="cardContent">
    <v-card
      class="mx-auto"
      color="#26c6da"
      dark
      max-width="500"
    >
    <v-card-title>
      <span class="title font-weight-bold"> {{ todo["title"] }}</span>
    </v-card-title>
    <v-card-text class="text font-weight-light">
      <h4> Description: {{ todo["description"] }}</h4>
      <h4> Point: {{ todo["point"] }}</h4>
      <h4> Assigned To: {{ todo["assignedTo"] }}</h4>
    </v-card-text>
    <v-card-actions>
      <v-layout wrap
        align-center
        justify-end
      >

      <v-btn class="error" @click="removeItem(todo)">
        DEL
      </v-btn>
      <v-btn class="warning" v-if="buttonPrev" @click="toPrev(todo)">
        Prev
      </v-btn>
      <v-btn class="success" v-if="buttonNext" @click="toNext(todo)">
        Next
      </v-btn>

      </v-layout>
    </v-card-actions>


    </v-card>
  </div>
</template>

<script>
  import db from '@/firebase.js'

  export default {
    props: ['todo', 'name'],
    data() {
      return {
        buttonNext: '',
        buttonPrev: '',
        kanbans: ['BackLog', 'ToDo', 'OnGoing', 'Finished']
      }
    },
    methods: {
      removeItem(todo) {
        db.collection("todos")
          .doc(todo.id)
          .delete()
          .then(() => {
            console.log(`Document successfully deleted!`)
          })
          .catch(err => {
            console.log(`Error removing document ${err}`)
          })

      },
      toNext(todo) {
        let newStatus = this.buttonNext
        db.collection("todos").doc(todo.id)
          .update({
            status: newStatus
          })
      },

      toPrev(todo) {
        let newStatus = this.buttonPrev
        db.collection("todos").doc(todo.id)
          .update({
            status: newStatus
          })

      }
    },
    created() {
      // console.log(JSON.stringify(this.todo))
      // console.log(this.data);
      // console.log(this.data.name, 'ini dia a    ajajajjajaja')
      // console.log(this.name, '++++++')
      if(this.name == 'BackLog') {
        this.buttonNext = 'ToDo',
        this.buttonPrev = null
      } else if(this.name == 'ToDo') {
        this.buttonNext = 'OnGoing',
        this.buttonPrev = 'BackLog'
      } else if(this.name == 'OnGoing') {
        this.buttonNext = 'Finished',
        this.buttonPrev = 'ToDo'
      } else if(this.name == 'Finished') {
        this.buttonNext = null
        this.buttonPrev = 'OnGoing'
      }
    }
  }

</script>

<style>

</style>
