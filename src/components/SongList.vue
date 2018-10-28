<template>
  <section>
    <md-list>
      <draggable v-model="songs" @start="drag=true" @stop="drag=false">
        <md-list-item v-for="song in songs" :key="song">
          <span class="md-list-item-text">{{song}}</span>
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
  }
}
</script>
