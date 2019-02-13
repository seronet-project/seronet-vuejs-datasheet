<template>
  <v-layout>
  <v-flex xs12 sm6 d-flex>
    <SelectClassR :headClass="headClass"  @update="returnSelectedClass"></SelectClassR>
    <SelectInstance :classId="classId" @update="returnSelectedInstance"/>
  </v-flex>

  <div v-for="sl in supportedLanguages" :key="sl.code">
    <v-btn color="success" @click="updateLang(sl.code)">{{sl.name}}</v-btn>
  </div>

</v-layout>
</template>

<script>
import gql from 'graphql-tag'
import SelectInstance from './SelectInstance'
import SelectClassR from './SelectClassR'

export default  {
  components: {
    SelectInstance, SelectClassR
  },
  props: ['componentId'],
  data() {
    return {
      localComponentId: this.componentId,
      classId: "http://seronet-projekt.de/models/t2#Gripper",
      headClass: "http://seronet-projekt.de/models/t1#HardwareComponent",
      grippers: [],
      sections: [{'name': 'test'}],
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

    async updateSections() {
      const query = gql`
        query User($componentId: ID!, $lang: SupportedLanguage) {
          getDatasheet(componentId:$componentId lang:$lang) {
            componentId
            createdAt
            sections {
              name
              mdicon
              fields {
                name
                value
                type
              }
            }
          }
        }
      `;
      const response = await fetch('http://' + process.env.VUE_APP_GRAPHQL_HOST, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Accept': 'application/json',
        },
        body: JSON.stringify({
          query,
          variables: { componentId: this.localComponentId, lang: this.lang },
        })
      });
      const {data} = await response.json()
      this.sections = data.getDatasheet ? data.getDatasheet.sections : []
      this.$emit('update', this.sections, this.localComponentId);
    },

    returnSelectedInstance(selectedComponentId){
      this.localComponentId = selectedComponentId
      this.updateSections()
    },

    returnSelectedClass(selectedClass){
      this.classId = selectedClass
    }
  },
  mounted() {
    this.updateSections()
  }
}
</script>
