<template>
  <div class="dashboard">
    <h1 class="subheading grey--text">Home</h1>
    <v-container class="my-5">
      <v-layout row class="mb-2">

          <v-tooltip top>
              <template #activator="data">
                  <v-btn small flat color="grey" v-on="data.on" v-on:click="sortBy('title')">
                      <v-icon left small>folder</v-icon>
                      <span class="caption text-lowercase">by project name</span>
                  </v-btn>
              </template>
              <span>Sort project by name</span>
          </v-tooltip>

          <v-tooltip top>
              <template #activator="data">
                  <v-btn small flat color="grey" v-on="data.on" v-on:click="sortBy('person')">
                      <v-icon left small>person</v-icon>
                      <span class="caption text-lowercase">by person</span>
                  </v-btn>
              </template>
              <span>Sort project by person</span>
          </v-tooltip>

      </v-layout>
      <v-card  v-for="project in projects" :key="project.title">
        <v-layout row wrap v-bind:class="`pa-3 project ${project.status}`">

          <v-flex xs12 md6>
            <div class="caption grey--text">Project Title</div>
            <div>{{project.title}}</div>
          </v-flex>

          <v-flex xs6 sm4 md2>
            <div class="caption grey--text">Person</div>
            <div>{{project.person}}</div>
          </v-flex>

          <v-flex xs6 sm4 md2>
            <div class="caption grey--text">Due by</div>
            <div>{{project.due}}</div>
          </v-flex>

          <v-flex xs2 sm4 md2>
            <v-chip :class="`${project.status} white--text caption my-2`" small>{{project.status}}</v-chip>
          </v-flex>

        </v-layout>
        <v-divider></v-divider>
      </v-card>
    </v-container>
  </div>
</template>

<script>
  import {eventBus} from '../main'
  export default {
    components: {

    },
    data(){
      return {
          projects:[
            { title: 'Design a new website', person: 'Aman', due: '1st Jan 2019', status: 'ongoing', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'},
            { title: 'Code up the homepage', person: 'Tansen', due: '10th Jan 2019', status: 'complete', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'},
            { title: 'Design video thumbnails', person: 'Roza', due: '20th Dec 2018', status: 'complete', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'},
            { title: 'Create a phone that doesn\'t suck', person: 'Bill Gates', due: '10th Oct 2018', status: 'overdue', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'},
            { title: 'Create a community forum', person: 'X-man', due: '20th Jan 2019', status: 'ongoing', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'},
            { title: 'Create a community forum', person: 'X-man', due: '20th Oct 2018', status: 'overdue', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'}
          ],
      }
    },
    methods:{
      sortBy(props){
          this.projects.sort((a,b)=>a[props]<b[props]? -1:1);
      }
    }
  }
</script>

<style scope>
.project.complete{
  border-left:4px solid #3cd1c2;
}
.project.ongoing{
  border-left:4px solid orange;
}
.project.overdue{
  border-left:4px solid tomato;
}

.v-chip.complete{
  background:#3cd1c2;
}
.v-chip.ongoing{
  background:orange;
}
.v-chip.overdue{
  background:tomato;
}
</style>
