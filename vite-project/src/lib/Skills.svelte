<script lang="ts">
</script>

<div class="skills-container">
    <div class="dashbox" style="width: 50vw; align-items: center;">
        <h2 style="color: #99cc99; font-size: 2.5em;">My Most-Used Technologies</h2>
    </div>

    <div style="display: flex; flex-direction: row; margin-top: 2em;">
        <div class="bg-red skill-bubble">
            <h3>TypeScript</h3>
        </div>
        <div class="bg-orange skill-bubble">
            <h3>Svelte</h3>
        </div>
        <div class="bg-yellow skill-bubble">
            <h3>Express</h3>
        </div>
        <div class="bg-green skill-bubble">
            <h3>SQL</h3>
        </div>
        <div class="bg-blue skill-bubble">
            <h3>React</h3>
        </div>
        <div class="bg-indigo skill-bubble">
            <h3>Tailwind CSS</h3>
        </div>
        <div class="bg-violet skill-bubble">
            <h3>HTML</h3>
        </div>
    </div>
</div>

<style>
    .skills-container {
        position: relative;
        align-self: center;
        margin-bottom: 2em;

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .dashbox {
        border: dashed 0.33em;
        border-color: #48454744;

        width: 30em;
    }

    .skill-bubble {
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;

        width: 10em;
        height: 10em;
        margin: 1em;
        border-radius: 50%;

        transition: transform 0.2s ease-in-out;
    }

    .skill-bubble:hover {
        cursor: default;

        transform: scale(1.2) rotate(3deg);
        transition: transform 0.1s ease-out;

        box-shadow: 0 2px 4px #48454744;
    }

    .shaker {
        animation-name: shake;
        animation-duration: 1s;
        animation-iteration-count: infinite;
        animation-timing-function: linear;
    }

    .bg-green {
        background-color: #99cc99;
    }

    .bg-blue {
        background-color: #99ccc5;
    }

    .bg-indigo {
        background-color: #99a8cc;
    }

    .bg-violet {
        background-color: #b699cc;
    }

    .bg-red {
        background-color: #cc99b6;
    }

    .bg-orange {
        background-color: #cca899;
    }

    .bg-yellow {
        background-color: #c5cc99;
    }

    @keyframes shake {
        0% {
            transform: rotate(0deg);
        }
        10% {
            transform: rotate(2.5deg);
        }
        20% {
            transform: rotate(5deg);
        }
        30% {
            transform: rotate(2.5deg);
        }
        40% {
            transform: rotate(0deg);
        }
        50% {
            transform: rotate(-2.5deg);
        }
        60% {
            transform: rotate(-5deg);
        }
        70% {
            transform: rotate(-2.5deg);
        }
        80% {
            transform: rotate(0deg);
        }
        90% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(0deg);
        }
    }

</style>
