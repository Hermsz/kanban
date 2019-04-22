<template>
  <div class="card">
    <v-container grid-list-md text-xs-center>
      <v-layout row wrap>
        <v-flex xs12>
          <v-flex>
            <v-card >
      <v-card-title
      >{{ data.name }}
      </v-card-title>
      <ContentCard 
        v-for="(todo, index) in data.tasks" 
        :key="index"
        :todo="todo"
        :name="name"
        ma-3
        >
      </ContentCard>

            </v-card>
          </v-flex>

        </v-flex>
      </v-layout>
    </v-container>




  </div>
</template>

<script>
  import ContentCard from './ContentCard.vue'


export default {
  props: ['data', 'name'],
  data() {
    return {
      color : ['red', 'indigo', 'blue', 'green']
    }
  },
  name: 'KanbanCard',
  components: {
    ContentCard
  },
}
</script>

<style scoped>

</style>