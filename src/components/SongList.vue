<template>
  <section>
    <md-list>
      <draggable v-model="songs" @start="drag=true" @stop="drag=false">
        <md-list-item v-for="song in songs" :key="song.name">
          <div class="md-list-item-text">
            <span>{{song.name}}</span>
            <span>Last Practiced: {{song.lastPracticed | moment('Do MMM YYYY')}}</span>
          </div>

          <md-button v-on:click="say()">
            <md-icon>check</md-icon>
          </md-button>
        </md-list-item>
      </draggable>
    </md-list>

  </section>
</template>

<script>
import draggable from 'vuedraggable'

export default {
  name: 'SongList',
  components: {
      draggable
  },
  data() {
    return {
      songs: [
        {
          name: 'Blondie - Call Me',
          lastPracticed: new Date(2018,9,21)
        },
        {
          name: 'Alice In Chains - Man In A Box',
          lastPracticed: new Date(2018,9,22)
        },
        {
          name: 'Guns N Roses - Nightrain',
          lastPracticed: new Date(2018,9,21)
        },
        {
          name: 'Heart - Barracuda',
          lastPracticed: new Date(2018,9,21)
        },
        {
          name: 'Alter Bridge - Blackbird',
          lastPracticed: new Date(2018,9,21)
        },
        {
          name: 'Green Day - Longview',
          lastPracticed: new Date(2018,9,21)
        },
        {
          name: 'Foo Fighters - The Pretender',
          lastPracticed: new Date(2018,9,21)
        },
        {
          name: 'Muse - Hysteria',
          lastPracticed: new Date(2018,9,21)
        },
        {
          name: 'Black Stone Cherry - Blind Man',
          lastPracticed: new Date(2018,9,21)
        },
        {
          name: 'Jane\'s Addiction - Been Caught Stealing',
          lastPracticed: new Date(2018,9,21)
        }
      ]
    }
  },
  methods: {
    say() {
      alert('innit')
    },
    updatePracticeDate() {

    }
  }
}
</script>

<style>
.md-list-item:hover {
  background-color: #eee;
  cursor: pointer;
}
.sortable-chosen {
  opacity: 0.3;
}
</style>
