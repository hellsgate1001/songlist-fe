<template>
  <section>
    <md-list>
      <draggable v-model="songs" @start="drag=true" @stop="drag=false">
        <md-list-item v-for="song in songs" :key="song">
          <div class="md-list-item-text">
            <span>{{song}}</span>
            <span>Last Practiced: 21st Oct 2018</span>
          </div>

          <md-button v-on:click="say(event)">
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
        'Blondie - Call Me',
        'Alice In Chains - Man In A Box',
        'Guns N Roses - Nightrain',
        'Heart - Barracuda',
        'Alter Bridge - Blackbird',
        'Green Day - Longview',
        'Foo Fighters - The Pretender',
        'Muse - Hysteria',
        'Black Stone Cherry - Blind Man',
        'Jane\'s Addiction - Been Caught Stealing'
      ]
    }
  },
  methods: {
    say(event) {
      alert('innit')
      event.stopPropagation()
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
