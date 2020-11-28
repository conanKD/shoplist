<template>
  <div className="App">
    <Header />
    <EntryForm
      v-on:add-entry="addEntry"
    />
    <div className="sortButtons">
      <button v-on:click="() => sortList('ASC')" >&#10148;</button>
      <button v-on:click="() => sortList('DESC')" >&#10148;</button>
    </div>
    <EntryList
      className="entryList"
      v-bind:entryList="entrys"
      v-on:del-entry="deleteEntry"
      v-on:toggle-completed="toggleCompleted"
    />
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import EntryForm from "./components/EntryForm";
import EntryList from "./components/EntryList";

export default {
  name: 'app',
  components: {
    Header,
    EntryForm,
    EntryList
  },
  data(){
    return{
      entrys: [ ]
    }
  },
  methods:{
    //Remove entry based on id
    deleteEntry(id){
      this.entrys = this.entrys.filter(entry => entry.id !== id);
    },
    //Toggle completed based on passed id
    toggleCompleted(id){
      this.entrys = this.entrys.map(entry =>{
        if(entry.id === id){
          return {...entry, completed: !entry.completed}
        }
        return entry;
      })
    },
    //Add entry to existing entrys
    addEntry(newObj){
      this.entrys = [...this.entrys, newObj];
    },
    //Sort based on direction
    sortList(direction){
      var sort;
      switch (direction) {
        case 'ASC':
          sort = (a, b) => a.title.localeCompare(b.title, 'de', {numeric:true});
          break;
        case 'DESC':
          sort = (a, b) => b.title.localeCompare(a.title, 'de', {numeric:true});
          break;
        default:
          sort = (a, b) => a.title.localeCompare(b.title, 'de', {numeric:true});
      }
      var newData = this.entrys.sort(sort);
      //replace entrys with new sorted entrys
      this.entrys = newData.map(entry =>{
        return entry
      });
    }
  }
}
</script>

<style lang="scss">
  :root{
    --bord-radius: 4px;
    --background: #ffffff;
    --text: #414856;
    --check: #4F29F0;
    --disabled: #C3C8DE;
    --width: 16em;
    --height: 100%;
    --border-radius: 10px;
  }
  body {
    background: #E8EBF3;
    height: 100vh;
    font: 400 20px 'Varela Round', sans-serif;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .header{
    color: black;
    text-align: center;
    padding: 12px;
  }

  .App {
    text-align: center;
    //background-color: #282c34;
    min-height: 100vh;
    height: 100%;
    background: var(--background);
    width: var(--width);
    height: var(--height);
    border-radius: var(--border-radius);
    position: relative;
    box-shadow: 0 10px 30px rgba(#414856, 0.05);
    padding: 30px 45px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .App-header{
    height: 90%;
  }

  .clickbox{
    margin-top:6px;
    margin-right: 5px;
  }

  input[name="title"]{
    border: 1px solid black;
    padding: 10px;
    border-right: none;
    border-top-left-radius: var(--bord-radius);
    border-bottom-left-radius: var(--bord-radius);
  }

  .btn{
    border: 1px solid blue;
    padding:10px 15px;
    background-color:blue;
    border-top-right-radius: var(--bord-radius);
    border-bottom-right-radius: var(--bord-radius);
    color: white;
  }
  .btn:focus{
    border:none;
  }
  .btn:hover{
    background-color:#2626c3;
  }

  .sortButtons{
    display: flex;
    margin-top: 0.5em;
    justify-content: space-evenly;
    flex-flow: row nowrap;
    width: 38%;
  }

  .sortButtons button{
    padding: 10px;
    font-size: 0.8em;
  }

  .sortButtons button:first-child{
  transform: rotate(-90deg);
  }
  .sortButtons button:last-child{
  transform: rotate(90deg);
  }

  .entryList{
    list-style-type:none;
    margin-left: auto;
    margin-right: auto;
    padding: 0;
    width: 50%;
    height: 18em;
    overflow: auto;
  }

  .entryList div {
    display: flex;
  }
  span.material-icons{
    cursor:pointer;
    text-decoration: none !important;
  }
  .entry-item p{
    display: flex;
    margin-bottom:0;
    margin-top: 0.5em;
  }
  input[type="checkbox"]{
    margin-top: 6px;
    margin-right: 10px;
  }

  li{
    color: black;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    //color: #2c3e50;
    margin-top: 60px;
  }

  //.btn{
  //  display:inline-block;
  //  border:none;
//    background:#555;
//    color:#fff;
//    padding: 7px 20px;
//  }
//  .btn:hover{
//    background: #666;
//  }
</style>
