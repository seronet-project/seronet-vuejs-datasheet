<template lang="html">
<v-layout row wrap>
  <v-container grid-list-md text-xs-center>
    <!-- 75-100=> lg, 110-125=> md, 150-200=> sm, 250=>xs -->
    <v-flex xl6 lg12 md12 sm10 xs12 offset-lg1 offset-sm1 offset-xl3>
      <div class="display-1 title-costum">Component Example Datasheet</div>
        <v-card class="mt-1">
          <br>
          <v-flex xs9 sm5 offset-sm7>
            <v-img
              v-bind:src="info.data.component.image"
              width="200px"
            ></v-img>
          </v-flex>
          <!-- <v-divider/> -->
          <!-- <v-flex xs4 sm4 offset-sm1 style="background-color:red;">
              <div class="display-1">
                  {{info.data.component.name}}
              </div>
              <div>test</div>
              <v-img src="https://www.robotnik.eu/web/wp-content/uploads//2015/11/RB-1-BASE-frontal.png"
              style="float:right;" width="200px"/>
          </v-flex> -->

          <v-layout row wrap>
            <!-- <v-flex v-for="i in 3" :key="`4${i}`" xs4>
              <v-card dark color="primary">
                <v-card-text class="px-0">{{info.data.component.name}}</v-card-text>
              </v-card>
            </v-flex> -->

            <v-flex xs7>
              <!-- <v-card flat dark color="primary"> -->
                <v-card-text class="text-xs-left display-1">{{info.data.component.name}}</v-card-text>
              <!-- </v-card> -->
            </v-flex>

            <v-flex xs1>
              <v-card dark color="primary">
                <!-- <v-card-text class="px-0">4</v-card-text> -->
              </v-card>
            </v-flex>

            <v-flex xs4>
              <!-- <v-card dark color="primary"> -->
                <v-img src="https://www.robotnik.eu/web/wp-content/uploads//2015/11/RB-1-BASE-frontal.png"/>
              <!-- </v-card> -->
            </v-flex>
            <br>
          </v-layout>

        <!-- <v-flex xs4>
          <v-card dark color="secondary">
          <v-card-title class="headline">
            {{info.data.component.name}}
          </v-card-title>
        </v-card>
        <v-img v-bind:src="info.data.component.image" class="logo"/>
        </v-flex> -->

      <v-divider/>
      <v-layout row wrap>
        <v-flex xs6>
          <div><b>Component Attributes </b></div>
        </v-flex>
        <v-flex xs6>
          <div><b>Hardware Component Attributes </b></div>
        </v-flex>
      </v-layout>

        <v-layout row wrap>
          <v-flex xs2>
          <v-card-text>
            <p class="text-xa-right">Name:</p>
            <p class="text-xs-right">Manufacturer:</p>
            <p class="text-xs-right">Description:</p>
            <br>
            <p class="text-xs-right">Function (capabilities):</p>
            <p class="text-xs-right">Use cases:</p>

          </v-card-text>
        </v-flex>

        <v-flex xs4 class="text-xs-left">
          <v-card-text>
            <p class="text-xs-left"><b>{{info.data.component.name}}</b></p>
            <p class="text-xs-left"><b>Robotnik</b></p>
            <p class="text-xs-left"><b>Mobile Platform designed for indoor Applications</b></p>
            <p class="text-xs-left"><b>Function</b></p>
            <br>
            <p class="text-xs-left"><b>Logistics, Remote Monitoring, Research&Development, General Purposes</b></p>
          </v-card-text>
        </v-flex>

        <v-flex xs2>
        <v-card-text>
          <p class="text-xs-right">weight:</p>
          <p class="text-xs-right">Link:</p>
          <p class="text-xs-right">Processor:</p>
        </v-card-text>
      </v-flex>

      <v-flex xs4>
        <v-card-text>
          <p class="text-xs-left"><b>{{info.data.component.weight}}</b></p>
          <p class="text-xs-left"><a v-bind:href="info.data.component.link">Further specification</a></p>
          <p class="text-xs-left"><b>{{info.data.component.processor}} </b></p>
        </v-card-text>
      </v-flex>
        </v-layout>


      </v-card>
</v-flex>

<!-- <v-container grid-list-md text-xs-center>
  <v-layout row wrap>
    <v-flex xs12>
      <v-card dark color="primary">
        <v-card-text class="px-0">12</v-card-text>
      </v-card>
    </v-flex>
    <v-flex v-for="i in 2" :key="`6${i}`" xs6>
      <v-card dark color="secondary">
        <v-card-text class="px-0">6</v-card-text>
      </v-card>
    </v-flex>
    <v-flex v-for="i in 3" :key="`4${i}`" xs4>
      <v-card dark color="primary">
        <v-card-text class="px-0">4</v-card-text>
      </v-card>
    </v-flex>
    <v-flex v-for="i in 4" :key="`3${i}`" xs3>
      <v-card dark color="secondary">
        <v-card-text class="px-0">3</v-card-text>
      </v-card>
    </v-flex>
    <v-flex v-for="i in 6" :key="`2${i}`" xs2>
      <v-card dark color="primary">
        <v-card-text class="px-0">2</v-card-text>
      </v-card>
    </v-flex>
    <v-flex v-for="i in 12" :key="`1${i}`" xs1>
      <v-card dark color="secondary">
        <v-card-text class="px-0">1</v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</v-container> -->


</v-container>
</v-layout>
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

.title-costum {
  // color: red;
}

  .figcaption {
   float: right;
   width: 100px !important;
}

.logo {
  width: 200px;
}
</style>
