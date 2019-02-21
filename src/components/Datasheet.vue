<template>
<v-layout>
  <v-flex xs12 sm6 offset-sm3>
    <v-card>
      <v-toolbar :color="this.color" dark>
        <v-toolbar-title>Datasheet ({{componentId}})</v-toolbar-title>
        <v-spacer></v-spacer>
      </v-toolbar>
      <div v-for="(section, index) in sections" :key="index">
        <ds-section
          color="blue"
          v-bind="section"
        ></ds-section>
      </div>
    </v-card>
  </v-flex>
</v-layout>
</template>

<script>
import DsSection from './Section'
import gql from 'graphql-tag'

export default {
  components: {
    DsSection
  },
  props: {
    color: String,
    componentId: String
  },
  data() {
    return {
      sections: [],
      lang:"en",
      supportedLanguages: [
        { code: 'en', name: 'English' },
        { code: 'de', name: 'German' }
      ]
    }
  },
  watch: {
    componentId() {
      this.updateSections()
    }
  },
  methods: {
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
          variables: { componentId: this.componentId, lang: this.lang },
        })
      });
      const {data} = await response.json()
      this.sections = data.getDatasheet ? data.getDatasheet.sections : []
    },
  },
  mounted() {
    this.updateSections()
    }
}
</script>
