<script lang="ts">
    let slideIndex = 1;
    document.addEventListener("DOMContentLoaded", () => {
        showSlides(slideIndex);
    });

    // Next/previous controls
    function shiftSlides(n) {
        showSlides(slideIndex += n);
    }

    function showSlides(n) {
        let i: number;
        let slides: HTMLCollectionOf<HTMLElement> =
            document.getElementsByClassName("slide-tiny") as HTMLCollectionOf<HTMLElement>;
        if (n > slides.length) {slideIndex = 1}
        if (n < 1) {slideIndex = slides.length}
        for (i = 0; i < slides.length; i++) {
            slides[i].style.display = "none";
        }

        slides[slideIndex-1].style.display = "block";
    }
</script>

<div class="tinysteps-container">
    <div class="dashbox">
        <a href="https://github.com/mmibbetson/tinysteps" target="_blank">
            <h2 class="text-red" style="margin-bottom: 0; font-size: 2.5em;">
                Tiny Steps
            </h2>
        </a>

        <p class="description">
            A RESTful API service built for musicians and non-musicians as a utility to quickly and
            easily generate chord progressions according to the guidelines of western functional harmony.
            The service is built with TypeScript, Express, and SQLite3.
        </p>
        <p class="description" style="padding-top: 0;">
            Tiny Steps is clearly documented with ease-of-use in mind, and maintains encrypted user accounts
            so that users can save and re-acquire previous or self-submitted chord progressions in JSON format.
            The service currently exists only as a proof-of-concept, but it is
            rate-limited and robustly designed.
        </p>
    </div>

    <div class="image-slider">
        <div class="slide-tiny fade">
            <img src="api_example.webp" alt="Tiny Steps" style="width: 100%;"/>
            <div class="bottom-text">Example API Output</div>
        </div>
        <div class="slide-tiny fade">
            <img src="auth_example.webp" alt="api example" style="width: 100%;"/>
            <div class="bottom-text">Base64 Authentication</div>
        </div>
        <div class="slide-tiny fade">
            <img src="code_example.webp" alt="code example" style="width: 100%;"/>
            <div class="bottom-text">Code Sample</div>
        </div>
        <div class="prev" on:click={() => shiftSlides(-1)} on:keypress={() => shiftSlides(-1)}>&#10094;</div>
        <div class="next" on:click={() => shiftSlides(1)} on:keypress={() => shiftSlides(1)}>&#10095;</div>
    </div>
</div>

<style>
    .tinysteps-container {
        display: flex;
        flex-direction: row;

        position: relative;
        margin-left: 5vw;
        margin-right: 5vw;
        margin-bottom: 2em;

        width: 90vw;
    }

    .image-slider {
        position: relative;
        margin: auto;
        margin-left: 4em;
        margin-right: 0;

        width: 66vw;
    }

    .slide-tiny {
        display: none;
    }

    .prev, .next {
        cursor: pointer;
        position: absolute;
        top: 50%;
        width: auto;
        margin-top: -22px;
        padding: 16px;
        color: #f8f9fa;
        font-weight: bold;
        font-size: 18px;
        transition: 0.6s ease;
        border-radius: 0 3px 3px 0;
        user-select: none;
    }

    .next {
        right: 0;
        border-radius: 3px 0 0 3px;
    }

    .prev:hover, .next:hover {
        background-color: #484547;
    }

    .bottom-text {
        color: #f2f2f2;
        font-size: 15px;
        padding: 8px 12px;
        position: absolute;
        bottom: 8px;
        width: 100%;
        text-align: center;
    }

    .fade {
        animation-name: fade;
        animation-duration: 1.5s;
    }

    @keyframes fade {
        from {opacity: .4}
        to {opacity: 1}
    }

    .dashbox {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

        border: dashed 0.33em;
        border-color: #48454744;

        width: 44vw;
    }

    .text-red {
        color: #cc9999;
    }

    .description {
        padding: 1.5em;
    }
</style>
