<template>
  <div>
    <div v-bind:key="entry.id" v-for="entry in entryList">
      <Entry
        v-bind:entry="entry"
        v-on:del-entry="$emit('del-entry', entry.id)"
        v-on:toggle-completed="$emit('toggle-completed', entry.id)"
      />
    </div>
  </div>
</template>

<script>
import Entry from './Entry.vue';

export default{
  name: "EntryList",
  components:{
    Entry
  },
  props: ["entryList"]
}
</script>

<style scoped>

</style>
