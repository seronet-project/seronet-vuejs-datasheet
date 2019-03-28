<template>
<v-app>
  <Actionbar @update="returnInstances" />

<div class="text-xs-bottom">
<div class="text-xs-center">
  <v-pagination v-model="page" :length="paginationLength" :total-visible="7"/>
</div>
  <div v-for="(instance, index) in instances.slice(((page-1)*3), ((page-1)*3)+3)">
    <Datasheet :color="colors[index]" :componentId="instance" />
  </div>
</div>

</v-app>
</template>

<script>
import Datasheet from './components/Datasheet'
import Actionbar from './components/Actionbar'

export default {
  components: {
    Datasheet,
    Actionbar
  },
  data() {
    return {
      sections: [],
      page: 1,
      paginationLength: 1,
      instances: [],
      colors: ["red", "orange", "green"]
    }
  },
  methods: {
    returnInstances(instances) {
        this.instances = instances
        this.paginationLength = Math.round(this.instances.length / 5)
        this.page = 1
    }
  }
}
</script>
