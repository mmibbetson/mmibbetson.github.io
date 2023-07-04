<script lang="ts">
  import BurgerBottom from "./lib/BurgerBottom.svelte";
  import BurgerMiddle from "./lib/BurgerMiddle.svelte";
  import BurgerTop from "./lib/BurgerTop.svelte";

</script>

<header class="drop-shadow sticky">
  <h1 id="title">Matthew Mark Ibbetson ›
    <span class="text-green">Software Engineer,</span>
    <span class="text-purple">Sound Designer,</span>
    <span class="text-pink">Creator.<span class="blinker">&nbsp;│</span></span>
  </h1>
</header>

<div style="display: flex; border: dashed 0.33em; border-color: #48454744; width: 90vw; margin: auto; margin-top: 2em;">
  <div class="circular-image">
    <img src="../profile.webp" alt="My profile picture" id="profile-image"/>
  </div>

  <div style="margin: auto;">
    <p class="summary">
      Hello! My name is Matthew and I am a passionate software engineer. I have experience
      building web applications using modern technologies such as React and Express with TypeScript.
      I am also deeply interested in the future of web technologies and am actively learning and developing
      with Rust.
    </p>
    <br/><br/>
    <p class="summary">
      Outside of software, I also compose and produce ambient, glitch, and experimental music.
      I have extended my sound design skills to the world of game development, and have worked on
      multiple game jam projects, as well as an independent Sci-fi animation project.
    </p>
  </div>
</div>

<div style="display: flex; flex-direction: column; align-items: left; margin-top: 2em;">
  <BurgerTop/>
  <BurgerMiddle/>
  <BurgerBottom/>
</div>

<footer style="display: flex; flex-direction: column; align-items: center;">
  <h2>Get In Touch:</h2>
      <button class="bg-green" style="position: relative; left: -4em;">
        <a href="mailto:mmibbetson@gmail.com" target="_blank">
          Email
        </a>
      </button>
      <button class="bg-purple">
        <a href="https://github.com/mmibbetson" target="_blank">
          GitHub
        </a>
      </button>
      <button class="bg-pink" style="position: relative; left: 4em;">
        <a href="https://www.linkedin.com/in/matthew-ibbetson-42b55b260" target="_blank">
          LinkedIn
        </a>
      </button>
</footer>

<style>
  #title {
    width: 100vw;
  }

  .sticky {
    position: sticky;
    top: 0;
    background-color: #f8f9fa;

    z-index: 1;
  }

  .bg-green {
    background-color: #99cc99;
  }

  .bg-purple {
    background-color: #9999cc;
  }

  .bg-pink {
    background-color: #cc9999;
  }

  .text-green {
    color: #99cc99;
  }

  .text-purple {
    color: #9999cc;
  }

  .text-pink {
    color: #cc9999;
  }

  .blinker {
    animation: blink 1s step-end infinite;
  }

  #profile-image {
    display: inline-flex;
    padding: 0.5em;
    width: 20em;
  }

  .summary {
    display: inline-flex;
    margin: auto;
  }

  .circular-image {
    width: 18em;
    height: 18em;
    border-radius: 50%;
    overflow: hidden;

    margin: 2em;
  }

  .circular-image img {
    position:relative;
    top: -20%;
    left: -5%;

    width: 100%;
    height: auto;
  }


  .drop-shadow {
    box-shadow: 0 2px 4px #48454744;
  }

  @keyframes blink {
    50% {
      opacity: 0;
    }
  }
</style>
