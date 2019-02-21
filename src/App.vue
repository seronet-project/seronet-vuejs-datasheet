<template>
<v-app>
  <Actionbar @update="returnInstances" />

  <!--  Actionbar: returns List of Components-->

  <!-- <v-pagination v-model="page" :length="paginationLength"></v-pagination> -->

  <!-- <div v-for="Instance in instances.slice(page*5,(page*5)+5)"> -->
  <div v-for="Instance in instances.slice(0, 2)">
    {{Instance}}
    <!-- {{page*5}}
    {{(page*5)+ 5}} -->
    <Datasheet color="pink" :componentId="Instance" />
  </div>

</v-app>
</template>

<script>
import Datasheet from './components/Datasheet'
import Actionbar from './components/Actionbar'

export default {
  components: {
    Datasheet,
    Actionbar
  },
  data() {
    return {
      sections: [],
      page: 1,
      array: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
      paginationLength: 0,
      instances: ["http://servicerobotik-ulm.de/ComponentsAndSystems#SmartCdlServer"]
    }
  },
  methods: {
    returnInstances(instances) {
        this.instances = instances
    }
  },
  mounted() {
    this.paginationLength = Math.round(this.array.length / 5)
  }
}
</script>
