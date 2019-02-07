<template>
  <v-layout>
    <!-- <div v-for="sl in supportedLanguages" :key="sl.code">
      <v-btn color="success" @click="updateLang(sl.code)">{{sl.name}}</v-btn>
    </div>
    <v-btn color="error" @click="updateSections()">Update</v-btn>
    <v-flex xs12 sm6 d-flex>
      <v-select v-model="componentId"
      @change="updateSections()"
      :items="grippers"
      box
      label="List Grippers"
      ></v-select>
    </v-flex> -->

    <!-- Datasheet starts here -->
    <v-flex xs12 sm6 offset-sm3>
      <v-card>
        <v-toolbar color="pink" dark>
          <v-toolbar-side-icon></v-toolbar-side-icon>
          <v-toolbar-title>Component Datasheet ({{componentId}})</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon>
            <v-icon>search</v-icon>
          </v-btn>
          <v-btn icon>
            <v-icon>check_circle</v-icon>
          </v-btn>
        </v-toolbar>

        <template v-for="section in sections">
          <div :key="section.name">
            <v-toolbar color="blue" dark>
              <v-icon>{{section.mdicon}}</v-icon>
              <v-spacer></v-spacer>
              <v-toolbar-title>
                {{section.name}}
              </v-toolbar-title>
              <v-spacer></v-spacer>
            </v-toolbar>
            <v-list two-line>
              <template v-for="(field, i) in section.fields">
                <div :key="field.name + i">
                  <v-list-tile avatar ripple>

                    <url-field v-if="field.type == 'URL'" :field="field"/>
                    <logo-field v-else-if="field.type == 'LOGO'" :field="field"/>
                    <image-field v-else-if="field.type == 'IMAGE'" :field="field"/>
                    <quantity-field v-else-if="field.type == 'QUANTITY'" :field="field"/>
                    <simple-field v-else :field="field"/>

                    <v-list-tile-action>
                      <v-list-tile-action-text>{{field.type}}</v-list-tile-action-text>
                    </v-list-tile-action>
                  </v-list-tile>
                  <v-divider/>
                </div>
              </template>
            </v-list>
          </div>
        </template>
      </v-card>
    </v-flex>
  </v-layout>
</template>
<script>
// import gql from 'graphql-tag'

import ImageField from './ImageField'
import UrlField from './UrlField'
import SimpleField from './SimpleField'
import LogoField from './LogoField'
import QuantityField from './QuantityField'

export default  {
  components: {
    ImageField, LogoField, UrlField, SimpleField, QuantityField
  },
  props: ['componentId', 'sections'],
  data() {
    return {
      // grippers: [],
      // sections: [],
    }
  },
  // methods: {
  //   updateLang(langCode) {
  //     this.lang = langCode
  //     this.updateSections()
  //     this.listGrippers()
  //   },
  //
  //   async updateSections() {
  //     const query = gql`
  //       query User($componentId: ID!, $lang: SupportedLanguage) {
  //         getDatasheet(componentId:$componentId lang:$lang) {
  //           componentId
  //           createdAt
  //           sections {
  //             name
  //             mdicon
  //             fields {
  //               name
  //               value
  //               type
  //             }
  //           }
  //         }
  //       }
  //     `;
  //     const response = await fetch('http://' + process.env.VUE_APP_GRAPHQL_HOST, {
  //       method: 'POST',
  //       headers: {
  //         'Content-Type': 'application/json',
  //         'Accept': 'application/json',
  //       },
  //       body: JSON.stringify({
  //         query,
  //         variables: { componentId: this.componentId, lang: this.lang },
  //       })
  //     });
  //     const {data} = await response.json()
  //     this.sections = data.getDatasheet ? data.getDatasheet.sections : []
  //   },
  //
  //   async listGrippers() {
  //     const query = gql`
  //       query User($classId: ID!) {
  //         getInstances(classId:$classId)
  //       }
  //     `;
  //     const response = await fetch('http://' + process.env.VUE_APP_GRAPHQL_HOST, {
  //       method: 'POST',
  //       headers: {
  //         'Content-Type': 'application/json',
  //         'Accept': 'application/json',
  //       },
  //       body: JSON.stringify({
  //         query,
  //         variables: { classId: "http://seronet-projekt.de/models/t2#Gripper"},
  //       })
  //     });
  //     const {data} = await response.json()
  //     this.grippers = data.getInstances
  //   }
  // },
  // mounted() {
  //   this.updateSections()
  //   this.listGrippers()
  // }
}
</script>
