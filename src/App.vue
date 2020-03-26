<template>
  <div id="app">
    <header>
      <h2>Befied</h2>
    </header>
    <main>
      <section class>
        <h2 class="song-title">
          {{current.title}} -
          <span>{{current.artist}}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>My playlist</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="(song.src === current.song ? 'song playing': 'song')"
        >{{song.title}} - {{song.title}}</button>
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
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
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
