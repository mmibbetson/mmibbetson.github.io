<script>

</script>

<div class="tinysteps-container">
    <div class="dashbox">
        <a href="https://github.com/mmibbetson/tinysteps" target="_blank">
            <h2 class="text-red">
                Tiny Steps
            </h2>
        </a>

        <p class="description">
            A RESTful API service built for musicians and non-musicians as a utility to quickly and
            easily generate chord progressions according to the guidelines of western functional harmony.
            The service is built with TypeScript, Express, and SQLite3.
        </p>

        <p class="description">
            Tiny Steps is clearly documented with ease-of-use in mind, and maintains encrypted user accounts
            so that users can save and re-acquire previous or self-submitted chord progressions in JSON format.
            Although the service currently exists only as a proof-of-concept and is not hosted, it is
            rate-limited and robustly designed.
        </p>
    </div>
</div>

<style>
    .tinysteps-container {
        position: relative;
        left: 5vw;
        margin-bottom: 2em;

        width: 95vw;
    }

    .dashbox {
        border: dashed 0.33em;
        border-color: #48454744;

        width: 30em;
    }

    .text-red {
        color: #cc9999;
    }

    .description {
        padding: 1em;
    }
</style>
