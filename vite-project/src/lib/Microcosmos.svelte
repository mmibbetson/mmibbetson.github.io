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
            document.getElementsByClassName("slide-micro") as HTMLCollectionOf<HTMLElement>;
        if (n > slides.length) {slideIndex = 1}
        if (n < 1) {slideIndex = slides.length}
        for (i = 0; i < slides.length; i++) {
            slides[i].style.display = "none";
        }

        slides[slideIndex-1].style.display = "block";
    }
</script>

<div class="microcosmos-container">
    <div class="image-slider">
        <div class="slide-micro fade">
            <img src="api_example.webp" alt="Tiny Steps" style="width: 100%;"/>
            <div class="bottom-text">Example API Output</div>
        </div>
        <div class="slide-micro fade">
            <img src="auth_example.webp" alt="api example" style="width: 100%;"/>
            <div class="bottom-text">Base64 Authentication</div>
        </div>
        <div class="slide-micro fade">
            <img src="code_example.webp" alt="code example" style="width: 100%;"/>
            <div class="bottom-text">Code Sample</div>
        </div>
        <div class="prev" on:click={() => shiftSlides(-1)} on:keypress={() => shiftSlides(-1)}>&#10094;</div>
        <div class="next" on:click={() => shiftSlides(1)} on:keypress={() => shiftSlides(1)}>&#10095;</div>
    </div>

    <div class="dashbox">
        <a href="https://microcosmos.live" target="_blank">
            <h2 class="text-purple" style="margin-bottom: 0; font-size: 2.5em;">
                Microcosmos
            </h2>
        </a>

        <p class="description">
            A web application built with TypeScript, React, .NET and AWS Lambda, Microcosmos is a tool for players
            of the popular MMORPG Final Fantasy XIV. It is a market board analysis tool that makes
            recommendations to players about what items to buy and sell for maximal profit.
        </p>

        <p class="description" style="padding-top: 0;">
            The need for the tool arose from the fact that the time required for the average player to
            manually analyze the market board and make decisions about what to craft or invest funds into
            was prohibitively high. As such, we designed Microcosmos to perform an
            algorithmic analysis at a set interval and ease users' cognitive load.
        </p>
    </div>
</div>

<style>
    .microcosmos-container {
        display: flex;
        flex-direction: row;

        position: relative;
        align-self: flex-end;
        margin-right: 5vw;
        margin-left: 5vw;
        margin-bottom: 2em;

        width: 90vw;
    }

    .dashbox {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        border: dashed 0.33em;
        border-color: #48454744;

        width: 40vw;
    }

    .text-purple {
        color: #9999cc;
    }

    .description {
        padding: 1.5em;
    }

    .image-slider {
        position: relative;
        margin: auto;
        margin-right: 4em;
        margin-left: 0;

        width: 60vw;
    }

    .slide-micro {
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
</style>
