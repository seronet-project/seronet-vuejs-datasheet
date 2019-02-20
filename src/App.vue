<template>
<v-app>
  <Actionbar :componentId="componentId" @update="returnSelectedClass" />

  <!--  Actionbar: returns List of Components-->

  <!-- <v-pagination v-model="page" :length="paginationLength"></v-pagination> -->

  <!-- <div v-for="field in array.slice(page*5,(page*5)+5)" :key="field.name"> -->
    <!-- {{page*5}}
    {{(page*5)+ 5}} -->
    <Datasheet color="pink" :componentId="componentId" :sections="sections" />
  <!-- </div> -->

</v-app>
</template>

<!-- DATASHEETS -->

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
      componentId: "http://servicerobotik-ulm.de/ComponentsAndSystems#SmartCdlServer",
      sections: [],
      page: 1,
      array: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
      paginationLength: 0
    }
  },
  methods: {
    returnSelectedClass(sections, componentId) {
      this.sections = sections,
        this.componentId = componentId
    }
  },
  mounted() {
    this.paginationLength = Math.round(this.array.length / 5)
  }
}
</script>
