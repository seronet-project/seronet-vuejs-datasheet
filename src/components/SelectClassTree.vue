<template>
<v-layout>
  <v-flex xs12 sm6 d-flex>
    <v-autocomplete v-model="localHeadClass" :items="this.subclasses" item-text="classId" box label="List Class"/>
  </v-flex>
</v-layout>
</template>

<script>
import gql from 'graphql-tag'

export default {
  props: ['headClass'],
  data() {
    return {
      subclasses: [],
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
      // for (var value in data.getSubclassesR[0].subclasses) {
      //   array[value] = data.getSubclassesR[0].subclasses[value]['classId'];
      // }

      console.log(this.subclasses);
    },
    returnSelectedClass() {
      this.$emit('update', this.localHeadClass);
    }
  },
  mounted() {
    this.listSubClasses()
  }
}
</script>
