<template>
  <section>
    <md-list>
      <md-subheader>
        <md-button v-on:click="addSong()">
          Add New Song <md-icon>add</md-icon>
        </md-button>
      </md-subheader>
      <md-list-item v-for="song in songs" :key="song.name">
        <div class="md-list-item-text">
          <span>{{song.name}}</span>
          <span>Last Practiced: {{song.lastPracticed | moment('Do MMM YYYY')}}</span>
        </div>

        <md-button v-on:click="say()">
          <md-icon>check</md-icon>
        </md-button>
      </md-list-item>
    </md-list>

  </section>
</template>

<script>
export default {
  name: 'SongList',
  data() {
    return {
      songs: []
    }
  },
  methods: {
    say() {
      alert('innit')
    },
    addSong() {
      const songName = prompt('Enter the song (Format: <Band Name> - <Song Name>)')
      if (songName != null && songName != '') {
        const data = {
          name: songName
        }
        this.$http.post('http://192.168.1.20:5000/add_song', JSON.stringify(data)).
        then((response) => {
          this.songs = response.body
        }, (error) => {
          alert('Some error occurred')
          // eslint-disable-next-line
          console.log(error)
        })
      }
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
