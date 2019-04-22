<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>BAM BAM</span>
        <span class="font-weight-light"> KAN BAN </span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        flat
        target="_blank"
      >
      <AddTask></AddTask>
      </v-btn>
    </v-toolbar>

    <v-content>
      <router-view/>
    </v-content>

  </v-app>
</template>

<script>
import AddTask from '@/components/AddTask.vue'



export default {
  name: 'App',
  components: {
    AddTask
  },
  data () {
    return {
      //
    }
  }
}
</script>
