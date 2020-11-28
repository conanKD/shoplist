<template>
  <div class="entry-item">
    <p>
      <span
        v-on:click="$emit('del-entry', entry.id)"
        class="material-icons"
      >delete</span>
      <input type="checkbox"
      v-on:change="$emit('toggle-completed', entry.id)" >
      <span v-bind:class="{'is-complete': entry.completed}">{{entry.title}}</span>
    </p>
  </div>
</template>

<script>
export default{
  name: "Entry",
  props: ["entry"]
}

</script>

<style scoped>
  span{
    -webkit-touch-callout: none; /* iOS Safari */
      -webkit-user-select: none; /* Safari */
       -khtml-user-select: none; /* Konqueror HTML */
         -moz-user-select: none; /* Old versions of Firefox */
          -ms-user-select: none; /* Internet Explorer/Edge */
              user-select: none;
  }
  .is-complete{
    text-decoration: line-through;
  }

  .del {
    background: red;
    color:white;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }
</style>
