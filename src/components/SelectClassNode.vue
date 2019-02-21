<template>
<v-layout>
  <v-flex xs12 sm12 d-flex>
    <div v-if="getSubclassesLength()">
    <v-autocomplete v-model="selectedClass" :items="subclasses" item-text="classId" box label="List Class" return-object v-bind:readonly="readonly" v-on:change="changed()"/>
      <div v-if="selectedClass.subclasses">
        <node :classId="selectedClass.classId" :subclasses="selectedClass.subclasses" v-bind:readonly="false" @update="returnSelectedClass"/>
      </div>
    </div>
  </v-flex>
</v-layout>
</template>

<script>

export default {
  name: "node",
  props: ['subclasses', 'classId'],
  data() {
    return {
      selectedClass: "test",
      index: 0,
      componentKey: 0,
      readonly: false
    }
  },
  methods: {
    getSubclassesLength(){
      if (this.subclasses.length != 0) {
        return true
      } else {
        this.$emit('update', this.classId);
        // this.$forceUpdate()
        return false
      }
    },
    returnSelectedClass(classId){
      this.$emit('update', classId);
    },
    changed(){
      if (this.selectedClass.subclasses == []) {
        this.readonly = true
      } else {
        this.readonly = false
      }
    }
  },
  computed: {
  }
}
</script>
