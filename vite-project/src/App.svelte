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

<div style="display: flex; border: dashed 0.33em; border-color: #48454744; margin-left: 5vw; margin-right: 5vw; margin-top: 2em; margin-bottom: 2em;">
  <div style="margin: auto; display: flex;">
    <div class="circular-image">
      <img src="../profile.webp" alt="My face" id="profile-image"/>
    </div>
    <div style="margin-top: auto; margin-bottom: auto;">
      <p class="summary">
        Hello! My name is Matthew. I have experience
        building web applications using modern technologies such as React and Express with TypeScript.
        I am also deeply interested in the future of web technologies and am actively developing multiple projects
        with Go.
      </p>
      <br/><br/>
      <p class="summary" style="padding-top: 0;">
        Outside of software, I also compose and produce ambient and experimental music.
        I have extended my sound design skills to the world of game development, and have worked on
        multiple game jam projects, as well as an independent Sci-fi animation project.
      </p>
      <br/><br/>
      <p class="summary" style="padding-top: 0;">
        <a href="./Matthew Ibbetson CV 2023.pdf" target="_blank">
          <button>
            My CV is available here.
          </button>
        </a>
      </p>
    </div>
  </div>
</div>

<div style="display: flex; flex-direction: column; align-items: left; margin-top: 2em;">
  <Skills/>
  <Microcosmos/>
  <TinySteps/>
</div>

<footer>
  <h2>Get In Touch:</h2>

    <a href="mailto:mmibbetson@gmail.com" target="_blank" class="bg-green barlink wobbler">
        <div>
          <i class="fa-solid fa-envelope"/>
          <span style="margin-left: 0.2em;">Email</span>
        </div>
    </a>
    <a href="https://github.com/mmibbetson" target="_blank" class="bg-purple barlink wobbler">
      <div>
        <i class="fa-brands fa-github"/>
        <span style="margin-left: 0.2em;">GitHub</span>
      </div>
    </a>
    <a href="https://www.linkedin.com/in/matthew-ibbetson-42b55b260" target="_blank" class="bg-pink barlink wobbler">
      <div>
        <i class="fa-brands fa-linkedin-in"/>
        <span style="margin-left: 0.2em;">LinkedIn</span>
      </div>
    </a>

    <br/><br/>
</footer>

<style>
  #title {
    margin: auto;
  }

  .barlink {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;

    width: 100vw;
    height: 2em;

    font-size: 1.5rem;

    transition: background-color 0.1s ease-out;
  }

  .wobbler:hover div {
    animation: wobble 1s 1;
  }

  .sticky {
    position: sticky;
    top: 0;
    background-color: #f8f9fa;

    z-index: 1;
  }

  .bg-green {
    background-color: #f8f9fa;
    color: #99cc99;
  }

  .bg-green:hover {
    background-color: #99cc99;
    color: #484547;
  }

  .bg-purple {
    background-color: #f8f9fa;
    color: #9999cc;
  }

  .bg-purple:hover {
    background-color: #9999cc;
    color: #484547;
  }

  .bg-pink {
    background-color: #f8f9fa;
    color: #cc9999;
  }

  .bg-pink:hover {
    background-color: #cc9999;
    color: #484547;
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
    padding-left: 1.5em;
    padding-right: 1.5em;
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

  @keyframes wobble {
    0% {
      transform: rotate(0deg) translate(0px, 0px) scale(1);
    }
    10% {
      transform: rotate(-3deg) translate(-2px, 0px) scale(1.05);
    }
    20% {
      transform: rotate(0deg) translate(0px, 0px) scale(1.1);
    }
    30% {
      transform: rotate(2deg) translate(2px, 0px) scale(1.15);
    }
    40% {
      transform: rotate(0deg) translate(0px, 0px) scale(1.2);
    }
    50% {
      transform: rotate(-4deg) translate(-2px, 0px) scale(1.2);
    }
    100% {
      transform: rotate(0deg) translate(0px, 0px) scale(1);
    }
  }
</style>
