<script>

</script>

<div class="skills-container">
    <div class="dashbox">
        <h2 style="color: #99cc99;">My Most-Used Technologies</h2>
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

        width: 9em;
        height: 9em;
        margin: 1em;
        border-radius: 50%;
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
</style>
