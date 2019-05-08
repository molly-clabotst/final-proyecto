<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <TasksForm v-on:task-added="newTaskAdded"></TasksForm>
    <Playlist v-bind:tasks="tasks"></Playlist>
  </div>
</template>

<script>
  import TasksForm from './components/TasksForm.vue'
  import Playlist from './components/Playlist'
  export default {
    name: 'app',
    components: {
      TasksForm,
      Playlist
    },
    data(){
      return{
        tasks:[]
      }
    },
    methods:{
      newTaskAdded(task){
        this.tasks.push(task);
        var tisks = this.tasks;
        for (var i = 0; i < tisks.length; i++) {

          // console.log(this.tasks[i])
        }

        // add task to list of tasks
        //TODO: Add a sorting function to verify that tasks aren't happening concurrently
        // sort them according to when they start
        if(this.tasks.length>1)
        //TODO: Make two sort functions, one for seeing if one task starts before the other, and one for validating that one task ends before the other begins.

          this.tasks.sort(function (t1, t2) {
            let thing = t1.stert-t2.stert;
            if(thing<0){
              let otherThing = t1.end - t2.stert;
              if (otherThing>=0){
                //TODO: show user error message
                //TODO: how to prevent the entry from existing
                console.log("One task must end before the other begins")
              }
            }else if (thing===0){
              console.log("No multitasking allowed")
            } else {
              let otherThing = t2.end-t2.stert;
              if(otherThing>=0){
                console.log("One task must end before the other begins")
              }
            }
            return thing
          });
      }
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
