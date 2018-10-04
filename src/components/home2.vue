<template lang="html">
<v-container>
    <!-- <v-btn color="success" v-on:click="getData">getData</v-btn> -->
    <!-- <v-alert :value="true" type="success">
    The button above has been clicked {{ getData }} times.
    </v-alert> -->
  <div class="title">Moving Platform Datasheet</div>
      <v-card class="mt-1">
        <v-img v-bind:src="info.data.component.image" style="width:200px"/>
        <v-card-title class="headline">
          {{info.data.component.name}}
        </v-card-title>
      <v-divider/>
        <v-card-text >
          weight: {{info.data.component.weight}} <br>
          <!-- <a href="{{info.data.component.link}}"></a> -->
          Link: <a v-bind:href="info.data.component.link">Further specification</a> <br>
          processor: {{info.data.component.processor}} <br>
          <!-- <img src="https://upload.wikimedia.org/wikipedia/commons/9/95/Vue.js_Logo_2.svg"/> -->
        </v-card-text>
        <v-card-text>
        </v-card-text>
        <v-img src="https://www.robotnik.eu/web/wp-content/uploads//2015/11/RB-1-BASE-frontal.png"
        style="float:right;" width="200px"/>
      </v-card>

</v-container>
</template>

<script lang="js">
  export default  {
    name: 'home-2',
    props: [],
    mounted() {
        var id1 = "a";
        // var id2 = "b";
        var query =
        `
        query User($id1: String){
          component(id: $id1){
            name
            weight
            link
            processor
            image
          }
        }`;
        fetch('http://localhost:4000/graphql', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Accept': 'application/json',
          },
          body: JSON.stringify({
            query,
            variables: { id1 },
          })
        }).then(r => r.json()).then(response => (this.info = response));

    },
    data() {
      return {
        counter: 0,
        data: 0,
        info: null,
        info2: null
      }
    },
    methods: {
    greet: function (event) {
     // `this` inside methods points to the Vue instance
     alert('Hello ' + this.name + '!')
     // `event` is the native DOM event
     if (event) {
       alert(event.target.tagName)
      }
    },
  },
    computed: {
    }
}
</script>

<style scoped lang="scss">
  .home-2 {
  }

  .figcaption {
   float: right;
   width: 100px !important;
}
</style>
