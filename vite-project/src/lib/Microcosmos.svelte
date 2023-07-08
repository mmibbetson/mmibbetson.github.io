<script>

</script>

<div class="microcosmos-container">
    <div class="dashbox">
        <a href="https://microcosmos.live" target="_blank">
            <h2 class="text-purple" style="margin-bottom: 0;">
                Microcosmos
            </h2>
        </a>

        <p class="description">
            A web application built with TypeScript, React, .NET and AWS Lambda, Microcosmos is a tool for players
            of the popular MMORPG Final Fantasy XIV. It is a market board analysis tool that makes
            recommendations to players about what items to buy and sell for maximal convenient profit.
        </p>

        <p class="description">
            The need for the tool arose from the fact that the time required for the average player to
            manually analyze the market board and make decisions about what to craft or invest funds into
            was prohibitively high. This is true even when considering the amazing, but complex, tools that
            exist for the community to do this analysis. As such, we designed Microcosmos to perform an
            algorithmic analysis at a set interval and make streamlined recommendations that users could trust
            would be relatively optimal.
        </p>
    </div>
</div>

<style>
    .microcosmos-container {
        position: relative;
        align-self: flex-end;
        margin-right: 5vw;
        margin-bottom: 2em;
    }

    .dashbox {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        border: dashed 0.33em;
        border-color: #48454744;

        width: 30em;
    }

    .text-purple {
        color: #9999cc;
    }

    .description {
        padding: 1em;
    }
</style>
