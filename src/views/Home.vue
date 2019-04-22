<template>
  <div class="home">
    <v-container>
      <div class="container-card">
        <KanbanCard v-for="(data, index) in taskLists" :key="index" :data="data" :name="data.name"></KanbanCard>
      </div>
    </v-container>
  </div>
</template>

<script>
  import KanbanCard from '@/components/KanbanCard.vue'
  import db from '@/firebase.js'


  export default {
    name: 'home',
    components: {
      KanbanCard
    },
    data() {
      return {
        taskLists: []
      }
    },
    created() {
      var docRef = db.collection("todos")

      docRef.onSnapshot(( querySnapshot ) =>  { // realtimenya kerja

        let taskData = [{
            name: 'BackLog',
            tasks: []
          },
          {
            name: 'ToDo',
            tasks: []
          },
          {
            name: 'OnGoing',
            tasks: []
          },
          {
            name: 'Finished',
            tasks: []
          }
        ]

        querySnapshot.forEach(element => {
          // console.log(element.data().status)
          // console.log(element.data())
          if(element.data().status == 'BackLog') {
            taskData[0].tasks.push({
              id: element.id,
              ...element.data()
            })
          } else if(element.data().status == 'ToDo') {
            taskData[1].tasks.push({
              id: element.id,
              ...element.data()
            })
          } else if(element.data().status == 'OnGoing') {
            console.log('masukkkk')
            taskData[2].tasks.push({
              id: element.id,
              ...element.data()
            })
          } else if(element.data().status == 'Finished') {
            taskData[3].tasks.push({
              id: element.id,
              ...element.data()
            })
          }
        });

        this.taskLists = taskData
      })
    }
  }

</script>
