<template>
  <div>
    <form v-on:submit.prevent="addEntry">
      <input
        type="text"
        v-model="title"
        name="title"
        placeholder="Add entry..."
        autocomplete="off"
      >
      <input type="submit" value="Submit" class="btn">
    </form>
  </div>
</template>


<script>
import { v4 as uuidv4 } from 'uuid';

export default{
  name: "EntryForm",
  data(){
    return{
      title: ''
    }
  },
  methods:{
    addEntry(){
      if(this.title){
        const newEntry = {
          id: uuidv4(),
          title: this.title,
          completed:false
        }
        this.$emit('add-entry', newEntry);
        this.title = '';
      }
    }
  }
}

</script>

<style scoped>
  form{
    display:flex
  }
  input[type="text"]{
    flex: 10;
    padding: 5px;
  }
  input[type="submit"]{
    flex: 2;
  }
</style>
