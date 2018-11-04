<template>
  <div>
    <div>
      <md-tabs md-active-tab="tab-current">
        <md-tab id="tab-current" md-label="Current" v-on:click="activate('tab-current')"></md-tab>
        <md-tab id="tab-new" md-label="New" v-on:click="activate('tab-new')"></md-tab>
      </md-tabs>
    </div>
    <section id="current" v-if="activeTab === 'tab-current'">
      <md-list>
        <md-list-item v-for="song in songs" :key="song.name">
          <div class="md-list-item-text">
            <span>{{song.name}}</span>
            <span>Last Practiced: {{song.lastPracticed | moment('Do MMM YYYY')}}</span>
          </div>

          <md-button v-on:click="setPracticed(song.name)">
            <md-icon>check</md-icon>
          </md-button>
        </md-list-item>
      </md-list>
    </section>

    <section id="tolearn" v-if="activeTab === 'tab-new'">
      <md-list>
        <md-subheader>
          <md-button v-on:click="addSong()">
            Add New Song <md-icon>add</md-icon>
          </md-button>
        </md-subheader>
        <md-list-item v-for="newSong in tolearn" :key="newSong">
          <div class="md-list-item-text">
            <span>{{newSong}}</span>
          </div>

          <md-button v-on:click="moveToCurrent(newSong)">
            <md-icon>add</md-icon>
          </md-button>
        </md-list-item>
      </md-list>
    </section>
  </div>
</template>

<script>
export default {
  name: 'SongList',
  data() {
    return {
      songs: [],
      tolearn: [],
      activeTab: 'tab-current'
    }
  },
  methods: {
    say() {
      alert('innit')
    },
    activate(tabName) {
      this.activeTab = tabName
    },
    setPracticed(name) {
      const data = {
        name: name
      }
      this.$http.post('http://192.168.1.20:5000/set_practiced', JSON.stringify(data)).
      then((response) => {
        this.songs = response.body
      }, (error) => {
        alert('Some error occurred - ' + error)
      })
    },
    addSong() {
      const songName = prompt('Enter the song (Format: <Band Name> - <Song Name>)')
      if (songName != null && songName != '') {
        const data = {
          name: songName
        }
        this.$http.post('http://192.168.1.20:5000/add_song', JSON.stringify(data)).
        then((response) => {
          this.tolearn = response.body.sort()
        }, (error) => {
          alert('Some error occurred')
          // eslint-disable-next-line
          console.log(error)
        })
      }
    },
    getSongs() {
      this.$http.get('http://192.168.1.20:5000/get_songs')
        .then((response) => {
          // eslint-disable-next-line
          console.log(response.body)
          this.songs = response.body.songs.sort(this.sortSongs)
          this.tolearn = response.body.tolearn.sort()
        }, (error) => {
          // eslint-disable-next-line
          console.log(error)
        })
    },
    moveToCurrent(name) {
      const data = {
        name: name
      }
      this.$http.post('http://192.168.1.20:5000/move_to_current', JSON.stringify(data)).
      then((response) => {
          this.songs = response.body.songs.sort(this.sortSongs)
          this.tolearn = response.body.tolearn.sort()
      }, (error) => {
        alert(error)
      })
    },
    sortSongs(a, b) {
      if (a.name < b.name) {
        return -1
      } else if (a.name > b.name) {
        return 1
      } else if (a.lastPracticed < b.lastPracticed) {
        return -1
      } else if (a.lastPracticed > b.lastPracticed) {
        return 1
      } else {
        return 0
      }
    }
  },
  beforeMount() {
    this.getSongs()
  }
}
</script>

<style>
.md-active {
  color: #448aff;
  border-bottom: solid 3px #448aff;
}
.md-list-item:hover {
  background-color: #eee;
  cursor: pointer;
}
.sortable-chosen {
  opacity: 0.3;
}
</style>
