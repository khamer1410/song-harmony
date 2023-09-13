<script lang="ts">
	import Butter from 'buttercms';
	import { onMount } from 'svelte';

	const butter = Butter(import.meta.env.VITE_APP_TITLE);
	let songData: any = {};


	onMount(() => {
		butter.content
			.retrieve(['song_harmony'])
			.then(function (resp) {
				const [song] = resp.data?.data.song_harmony || [];
				if (!song) throw new Error(`wrong song format, got ${resp}`);
				songData = song;
			})
			.catch(function (resp) {
				console.log(resp);
			});
	});

  // main button to play all tracks
  function playAll() {
      const audios = document?.querySelectorAll("audio");
      audios.forEach((audio) => audio.play());
    }

    function pauseAll() {
      const audios = document?.querySelectorAll("audio");
      audios.forEach((audio) => {
        audio.pause();
        audio.currentTime = 0;
      });
    }
</script>

<svelte:head>
	<title>Grace Kelly chorus voicing 🎵</title>
	<meta name="description" content="About this app" />
  <link
      href="https://fonts.googleapis.com/css2?family=Eczar&display=swap"
      rel="stylesheet"
    />
</svelte:head>

<div class="container cover">
	<h1>HEllo Butter CMS</h1>

	<h2>{songData.song_title}</h2>
	<p>{songData.lyrics}</p>
  <button class="button-three" on:click={playAll} type="button">
  PLAY
  </button>
  <button class="button-three" on:click={pauseAll} type="button">
    PAUSE
  </button>

  <section id="audio-wrapper" class="audio-wrapper glass">


  </section>

</div>

<footer>
	Made with use of
	<a href="http://buttercms.com">
		<img src="https://cdn.buttercms.com/JSSDbrHPSnGlLUcyHTn5" alt="butter logo" class="logo" />
	</a>
</footer>

<style>
	.container {
		flex-grow: 1;
	}

  .cover {
    background-image: url("https://media.npr.org/assets/music/news/2009/10/mika-7aef1e321cb7b8b6fe8397b01f0019cf55c038d3-s1100-c50.jpg");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  min-height: 100vh;
  font-family: "Eczar", serif;
  }

	footer {
		display: flex;
		justify-content: flex-end;
		align-items: center;
	}

	.logo {
		width: 260px;
	}

  .audio-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 30px;
  padding: 30px;
  margin-top: 20px;
}

.track {
  display: flex;
  align-content: center;
  justify-content: space-between;
  gap: 50px;
}

.glass {
  background: rgba(255, 255, 255, 0.3);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(3.5px);
  -webkit-backdrop-filter: blur(3.5px);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.18);
}

h1 {
  color: aliceblue;
}

button {
}

/* //codepen copypast */
.tgl {
  display: none;
}

.tgl::selection,
.tgl:after::selection,
.tgl:before::selection,
.tgl *::selection,
.tgl *:after::selection,
.tgl *:before::selection,
.tgl + .tgl-btn::selection {
  background: none;
}
.tgl + .tgl-btn {
  outline: 0;
  display: block;
  width: 8em;
  height: 2.5em;
  position: relative;
  cursor: pointer;
  user-select: none;
}
.tgl + .tgl-btn:after,
.tgl + .tgl-btn:before {
  position: relative;
  display: block;
  content: "";
  width: 50%;
  height: 100%;
}
.tgl + .tgl-btn:after {
  left: 0;
}
.tgl + .tgl-btn:before {
  display: none;
}
.tgl:checked + .tgl-btn:after {
  left: 50%;
}

.tgl-flip + .tgl-btn {
  padding: 2px;
  transition: all 0.2s ease;
  font-family: sans-serif;
  perspective: 100px;
}
.tgl-flip + .tgl-btn:after,
.tgl-flip + .tgl-btn:before {
  display: inline-block;
  transition: all 0.4s ease;
  width: 100%;
  text-align: center;
  position: absolute;
  line-height: 2em;
  font-weight: bold;
  color: #fff;
  position: absolute;
  top: 0;
  left: 0;
  backface-visibility: hidden;
  border-radius: 4px;
}
.tgl-flip + .tgl-btn:after {
  content: attr(data-tg-on);
  background: #02c66f;
  transform: rotateY(-180deg);
}
.tgl-flip + .tgl-btn:before {
  background: #ff3a19;
  content: attr(data-tg-off);
}
.tgl-flip + .tgl-btn:active:before {
  transform: rotateY(-20deg);
}
.tgl-flip:checked + .tgl-btn:before {
  transform: rotateY(180deg);
}
.tgl-flip:checked + .tgl-btn:after {
  transform: rotateY(0);
  left: 0;
  background: #7fc6a6;
}
.tgl-flip:checked + .tgl-btn:active:after {
  transform: rotateY(20deg);
}

/* button  */
.button-three {
  position: relative;
  background-color: #e0cfb3;
  border: none;
  padding: 20px;
  width: 200px;
  text-align: center;
  transition-duration: 0.4s;
  text-decoration: none;
  overflow: hidden;
  border-radius: 5px;
  margin: 5px;
}

.button-three:hover {
  background: #fff;
  box-shadow: 0px 2px 10px 5px #97b1bf;
  color: #000;
}

.button-three:after {
  content: "";
  background: #f1c40f;
  display: block;
  position: absolute;
  padding-top: 300%;
  padding-left: 350%;
  margin-left: -20px !important;
  margin-top: -120%;
  opacity: 0;
  transition: all 0.8s;
}

.button-three:active:after {
  padding: 0;
  margin: 0;
  opacity: 1;
  transition: 0s;
}
</style>
