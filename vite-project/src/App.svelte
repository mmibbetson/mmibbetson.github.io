<script lang="ts">
</script>

<header>
  <h1 id="title">Matthew Mark Ibbetson ›
    <span class="text-green">Software Engineer,</span>
    <span class="text-purple">Musician,</span>
    <span class="text-pink">Creator.<span class="blinker">&nbsp;│</span></span>
  </h1>
</header>

<img src="../profile.webp" alt="My profile picture" id="profile-image"/>

<p id="summary">
  Hello! My name is Matthew and I am a passionate software engineer. I have experience
  building web applications using modern technologies such as React and Express with TypeScript.
  I am also deeply interested in the future of web technologies and am actively learning and developing
  with Rust.
</p>
<br/>
<p>
  Outside of software, I also compose and produce ambient, glitch, and experimental music.
  I have extended my sound design skills to the world of game development, and have worked on
  multiple game jam projects, as well as an independent Sci-fi animation project.
</p>

<footer>
  <h2>Get In Touch:</h2>
  <ul>
    <li>
      <button class="bg-green">
        <a href="mailto:mmibbetson@gmail.com" target="_blank">
          Email
        </a>
      </button>
    </li>
      <li>
      <button class="bg-purple">
        <a href="https://github.com/mmibbetson" target="_blank">
          GitHub
        </a>
      </button>
    </li>
      <li>
      <button class="bg-pink">
        <a href="https://www.linkedin.com/in/matthew-ibbetson-42b55b260" target="_blank">
          LinkedIn
        </a>
      </button>
    </li>
  </ul>
</footer>

<style>
  #title {
    width: 100vw;
  }

  .bg-green {
    background-color: #8ed6a6;
  }

  .bg-purple {
    background-color: #A68ED6;
  }

  .bg-pink {
    background-color: #D6A68E;
  }

  .text-green {
    color: #8ed6a6;
  }

  .text-purple {
    color: #A68ED6;
  }

  .text-pink {
    color: #D6A68E;
  }

  .blinker {
    animation: blink 1s step-end infinite;
  }

  #profile-image {
    padding: 0.5em;
    width: 20em;
  }

  @keyframes blink {
    50% {
      opacity: 0;
    }
  }
</style>
