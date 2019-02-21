<template>
  <v-layout>
  <v-flex xs12 sm6 d-flex row>
    <SelectClassTree @update="returnSelectedClass"/>
    <SelectInstance :classId="classId" @update="returnInstances"/>
  </v-flex>

  <div v-for="sl in supportedLanguages" :key="sl.code">
    <v-btn color="success" @click="updateLang(sl.code)">{{sl.name}}</v-btn>
  </div>

</v-layout>
</template>

<script>
import SelectInstance from './SelectInstance'
import SelectClassTree from './SelectClassTree'

export default  {
  components: {
    SelectInstance, SelectClassTree
  },
  data() {
    return {
      selectedInstances: this.selectedInstances,
      classId: "",
      lang:"en",
      supportedLanguages: [
        { code: 'en', name: 'English' },
        { code: 'de', name: 'German' }
      ]
    }
  },
  methods: {
    updateLang(langCode) {
      this.lang = langCode
      this.updateSections()
      this.listInstances()
    },

    returnInstances(instances){
      this.selectedInstances = instances
      this.$emit('update', this.selectedInstances);
    },

    returnSelectedClass(selectedClass){
      this.classId = selectedClass
    }
  }
}
</script>
