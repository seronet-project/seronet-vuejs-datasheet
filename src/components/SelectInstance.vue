<template>
<v-layout>
  <v-flex xs12 sm6 d-flex>
    <v-autocomplete v-model="selectedInstance" @change="returnInstances()" :items="instances" box label="List Instances"/>
    <v-btn color="error" @click="removeInstance()">Remove</v-btn>
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
      selectedInstance: ''
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
      this.returnInstances()
    },
    returnInstances() {
      let submitArray = []
      if (this.selectedInstance != "") {
        submitArray[0] = this.selectedInstance
      } else {
        submitArray = this.instances
      }
      this.$emit('update',submitArray);
    },
    removeInstance(){
      this.selectedInstance = ""
      this.returnInstances()
    }
  },
  mounted() {
  }
}
</script>
