<template>
  <div id="app">
    <header>
      <h2>My Playlist</h2>
    </header>
    <main>
      <section class>
        <h2 class="song-title">
          {{current.title}} -
          <span>{{current.artist}}</span>
        </h2>
        <div class="controls">
          <button class="prev">Prev</button>
          <button class="play" v-if="!isPlaying">Play</button>
          <button class="pause" v-else>Pause</button>
          <button class="next">Next</button>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: "Even when it hurts",
          artist: "Hillsong",
          src: require("./assets/07-Even-When-It-Hurts.mp3")
        },
        {
          title: "Old church choir",
          artist: "Zach Williams",
          src: require("./assets/Zach-Williams-Old-Church-Choir.mp3")
        }
      ],
      player: new Audio()
    };
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    }
  },
  pause() {
    
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
