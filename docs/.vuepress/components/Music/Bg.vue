// Template
<template>
  <span class="music-player">
    <img :src="icon" class="playerComtrols" @click="musicHandler">
    <audio
      id="bg-music"
      class="bg-music"
      controls="false"
      autoplay="autoplay"
      loop
      download="false"
    >
      <source :src="$withBase('/time-travel.mp3')">
    </audio>
  </span>
</template>

// Script
<script>
const playIcon = require("../../../../assets/play.svg");
const pauseIcon = require("../../../../assets/pause.svg");

export default {
  data() {
    return {
      audio: null,
      playing: false
    };
  },
  computed: {
    icon() {
      return this.playing ? pauseIcon : playIcon;
    }
  },
  methods: {
    loadMusic() {
      if (!this.audio) {
        this.audio = document.getElementById("bg-music");
      }
      const musicInBrowserHandler = () => {
        if (this.audio && typeof this.audio.play == "function") {
          this.audio.play().catch(err => {
            /* eslint-disable */
            console.log(
              "%c     ",
              "background-image: url('http://media0.giphy.com/media/MOWPkhRAUbR7i/giphy.gif'); background-repeat: no-repeat; background-size: 250px 113px; font-size: 113px;",
              "Relaxed, There Is No Error, Just Need Some User Touch!",
              err
            );
            /* eslint-enable */
          });
        }
        this.playing = true;
        document.body.removeEventListener("click", musicInBrowserHandler);
      };
      document.body.addEventListener("click", musicInBrowserHandler);
    },
    musicHandler() {
      if (!this.audio) {
        return;
      }
      if (this.playing) {
        this.audio.pause();
        this.playing = false;
      } else {
        this.audio.play();
        this.playing = true;
      }
    }
  },
  mounted() {
    this.loadMusic();
  }
};
</script>

// Style
<style scoped>
.music-player {
  box-sizing: border-box;
  display: inline;
  align-items: center;
  position: relative;
  line-height: 2.2rem;
  margin-right: 3.2rem;
}
.bg-music {
  display: none;
}

.playerComtrols {
  position: absolute;
  height: 2rem;
}
</style>
