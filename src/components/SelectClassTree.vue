<template>
<v-layout>
  <v-flex xs12 sm6 d-flex>
    <SelectClassNode :classId="localHeadClass" :subclasses="this.subclasses" @update="returnSelectedClass"/></SelectClassNode>
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
      subclass: [],
      localHeadClass: this.headClass
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
            classId: this.headClass
          },
        })
      });

      const { data } = await response.json()
      this.subclasses = data.getSubclassesR[0].subclasses
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
