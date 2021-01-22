<template>
  <header>
    <h1>想见你歌单</h1>      
  </header>
  <main>
    <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <br>
      <section class="playlist">
        <h3>曲目</h3>
        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
          {{ song.title }} - {{ song.artist }}
        </button>
      </section>
      <small class="author">2021 @angelol2046</small>
  </main>
  
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {},
  data(){
    return{
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: '想见你想见你想见你',
          artist: '八三夭',
          src: require('./assets/xiangjianni.mp3')
        },
        {
          title: 'Someday or One Day',
          artist: '孙盛希 Shi Shi',
          src: require('./assets/somedayoroneday.mp3')
        },
        {
          title: '一天 Someday',
          artist: '黄宣 YELLOW',
          src: require('./assets/yitian.mp3')
        },
        {
          title: '看见你的声音 See Your Voice',
          artist: '陈零九 Nine Chen',
          src: require('./assets/kanjiannideshengyin.mp3')
        },
        {
          title: '逃',
          artist: '孙盛希',
          src: require('./assets/tao.mp3')
        },
        {
          title: 'Last Dance',
          artist: '伍佰 Wu Bai & China Blue',
          src: require('./assets/lastdance.mp3')
        },
        {
          title: '拥抱 Embrace',
          artist: '五月天 Mayday',
          src: require('./assets/yongbao.mp3')
        },
        {
          title: '秘密 Secret',
          artist: '张震嶽 A-Yue',
          src: require('./assets/mimi.mp3')
        },
        {
          title: '明天 Will We Remember?',
          artist: '杨乃文 Naiwen Yang',
          src: require('./assets/mingtian.mp3')
        },
        {
          title: 'The Last Waltz',
          artist: 'X-Ray Dog',
          src: require('./assets/thelastwaltz.mp3')
        },
        {
          title: 'Devoted',
          artist: 'X-Ray Dog',
          src: require('./assets/devoted.mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods:{
    play(song){
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener('ended', function () {
        this.index++;
        if (this.index > this.songs.length - 1) {
          this.index = 0;
        }
        this.current = this.songs[this.index];
        this.play(this.current);
      }.bind(this));
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    },
    next () {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev () {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }
}
</script>

<style>
*{
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
body {
	font-family: sans-serif;
}
header {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 15px;
	background-color: #212121;
	color: #FFF;
}
main {
  width: 100%;
  max-width: 2330px;
  margin: 0 auto;
  padding: 25px;
  background-image: url(./assets/image.jpg);
  text-align: center;
}
main:after{
  opacity: 0.1;
}
.song-title {
  color: #53565A;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.song-title span {
  font-weight: 400;
  font-style: italic;
}
.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
}
.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #FFF;
  background-color: #CC2E5D;
}
.next, .prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #FFF;
  background-color: #FF5858;
}
.playlist {
  padding: 0px 30px;
}
.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist .song:hover {
  color: #FF5858;
}
.playlist .song.playing {
  color: #FFF;
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}
.author {
  text-align: center;
  opacity: 0.4;
  margin-bottom: 10px;
}
</style>
