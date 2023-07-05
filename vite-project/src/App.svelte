<script lang="ts">
  import Skills from "./lib/Skills.svelte";
  import Microcosmos from "./lib/Microcosmos.svelte";
  import TinySteps from "./lib/TinySteps.svelte";

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
    <img src="../profile.webp" alt="My face" id="profile-image"/>
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
  <Skills/>
  <Microcosmos/>
  <TinySteps/>
</div>

<footer>
  <h2>Get In Touch:</h2>

    <a href="mailto:mmibbetson@gmail.com" target="_blank" class="bg-green barlink greenlink">
        <i class="fa-solid fa-envelope"/>
        <span style="margin-left: 0.2em;">Email</span>
    </a>
    <a href="https://github.com/mmibbetson" target="_blank" class="bg-purple barlink purplink">
      <i class="fa-brands fa-github"/>
      <span style="margin-left: 0.2em;">GitHub</span>
    </a>
    <a href="https://www.linkedin.com/in/matthew-ibbetson-42b55b260" target="_blank" class="bg-pink barlink pinklink">
      <i class="fa-brands fa-linkedin-in"/>
      <span style="margin-left: 0.2em;">LinkedIn</span>
    </a>
</footer>

<style>
  #title {
    width: 100vw;
  }

  .barlink {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;

    width: 100vw;
    height: 4em;

    font-size: 1.5rem;
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

  .greenlink:hover {
    background-color: #88bb88;
  }

  .bg-purple {
    background-color: #9999cc;
  }

  .purplink:hover {
    background-color: #8888bb;
  }

  .bg-pink {
    background-color: #cc9999;
  }

  .pinklink:hover {
    background-color: #bb8888;
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
