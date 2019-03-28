<template>
<v-layout>
  <v-flex xs12 sm12 d-flex>
    <div v-if="getSubclassesLength()">
    <v-autocomplete v-model="selectedClass" :items="subclasses" item-text="classId" box label="List Class" return-object/>
      <div v-if="selectedClass.subclasses">
        <node :classId="selectedClass.classId" :subclasses="selectedClass.subclasses" @update="returnSelectedClass"/>
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
    }
  },
  methods: {
    getSubclassesLength(){
      if (this.subclasses.length != 0) {
        return true
      } else {
        this.$emit('update', this.classId);
        return false
      }
    },
    returnSelectedClass(classId){
      this.$emit('update', classId);
    }
  }
}
</script>
