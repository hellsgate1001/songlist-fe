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
      songs: []
    }
  },
  methods: {
    say() {
      alert('innit')
    },
    getSongs() {
      this.$http.get('http://192.168.1.20:5000/update_practiced')
        .then((response) => {
          // eslint-disable-next-line
          console.log(response.body)
          this.songs = response.body
        }, (error) => {
          // eslint-disable-next-line
          console.log(error)
        })
    }
  },
  beforeMount() {
    this.getSongs()
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
