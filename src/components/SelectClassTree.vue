<template>
<v-layout row>
  <v-flex xs12 sm6>
    <SelectClassNode :classId="classId" :subclasses="this.subclasses" @update="returnSelectedClass"/>
  </v-flex>
</v-layout>
</template>

<script>
import gql from 'graphql-tag'
import SelectClassNode from './SelectClassNode'

export default {
  props: ['headClass'],
  components: {
    SelectClassNode
  },
  data() {
    return {
      subclasses: [],
      classId: "http://seronet-projekt.de/models/t1#Component"
    }
  },
  methods: {
    async listSubClasses() {
      const query = gql `
        query User($classId: ID!) {
          getSubclassesR(classId:$classId){
            classId, subclasses{classId, subclasses{classId, subclasses{classId, subclasses{classId}}}}
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
          variables: {
            classId: this.classId
          },
        })
      });
<<<<<<< HEAD:src/components/SelectClassTree.vue

      const { data } = await response.json()
      this.subclasses = data.getSubclassesR[0].subclasses
=======
      const {data} = await response.json()
      let array = []
      for (var value in data.getSubclassesR[0].subclasses) {
        array[value] = data.getSubclassesR[0].subclasses[value]['classId'];
      }
      this.subclasses = array
>>>>>>> master:src/components/SelectClassR.vue
    },
    returnSelectedClass(classId) {
      this.$emit('update',classId);
    }
  },
  mounted() {
    this.listSubClasses()
  }
}
</script>
