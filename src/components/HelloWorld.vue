<template>
  <v-container fluid>
    <v-slide-y-transition mode="out-in">
      <v-layout column align-center>
        <img src="@/assets/logo.png" alt="Vuetify.js" class="mb-5">
        <blockquote>
          &#8220;First, solve the problem. Then, write the code.&#8221;
          <footer>
            <small>
              <em>&mdash;John Johnson</em>
            </small>
          </footer>
        </blockquote>
      </v-layout>
    </v-slide-y-transition>
    <v-card>
     <v-card-text>
       <p class="text-lg-right">Right align on large viewport sizes</p>
       <p class="text-md-center">Center align on medium viewport sizes</p>
       <p class="text-sm-left">Left align on small viewport sizes</p>
       <p class="text-xs-center">Center align on all viewport sizes</p>
       <p class="text-xs-right">Right align on all viewport sizes</p>
     </v-card-text>
   </v-card>
  </v-container>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
