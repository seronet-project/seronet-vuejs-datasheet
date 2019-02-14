<template>
<v-layout>
  <v-flex xs12 sm6 d-flex>
    <v-autocomplete v-model="localComponentId" @change="returnSelectedInstance()" :items="instances" box label="List Instances"></v-autocomplete>
  </v-flex>
</v-layout>
</template>

<script>
import gql from 'graphql-tag'

export default {
  props: ['classId'],
  watch: {
    classId() {
      this.listInstances()
    }
  },
  data() {
    return {
      instances: [],
      localComponentId: ''
    }
  },
  methods: {
    async listInstances() {
      const query = gql `
        query User($classId: ID!) {
          getInstances(classId:$classId)
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
      const { data } = await response.json()
      this.instances = data.getInstances
    },
    returnSelectedInstance() {
      this.$emit('update', this.localComponentId);
    }
  },
  mounted() {
    this.listInstances()
  }
}
</script>
