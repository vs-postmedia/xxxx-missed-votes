<script>
    export let data = [];
    export let value = '';

    // LIBS
    import { onMount } from 'svelte';

    // VARS

    // FUNCTIONS
    function init() {
        console.log('CHART INIT!')
    }
    function addCommasToNumber(number) {
        return number.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }

    // LIGHTS! CAMERA! ACTION!
    onMount(init);
</script>


<div id="right-column">
    <div id="intro" class="step">
        <p>Mayor Ken Sim has been marked absent on city council votes far more often than previous mayors – and his current council members, too.</p>
        <p>The calendar to the right shows how many votes Sim missed on any given day since he was elected. Hover or tap a day to see how many times the mayor was marked “Absent.”</p>
    </div>
    <div id="mayor-chart" class="step">
        <iframe src='https://flo.uri.sh/visualisation/20404697/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='max-width:200px;height:150px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe>
    </div>
    <div id="council-chart" class="step">
        <p>The mayor missed more votes than his colleagues...</p>
        <iframe src='https://flo.uri.sh/visualisation/20404954/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='max-width:200px;height:350px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe>
    </div>
    <div id="summer23" class="step">
        <p>...and in the summer of 2023 he missed seven days of council meetings, totalling 81 votes.</p>
    </div>
    <div id="meeting-type" class="step">
        <p>The mayor is most likely to skip public hearings, which are often held in the evening.</p>
        <iframe src='https://flo.uri.sh/visualisation/20405084/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='max-width:180px;height:250px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe>
    </div>
    <div id="metro-meetings" class="step">
        <p>He isn’t just skipping council meetings, though. He’s only attended a quarter of the 41 Metro Vancouver XXX meetings.</p>
        <iframe src='https://flo.uri.sh/visualisation/20405301/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='max-width:180px;height:150px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe>
    </div>
    <div id="summer24" class="step">
        <p>Sim missed 114 votes in the summer of 2024 – the most intense period of missed votes of his tenure so far.</p>
    </div>
</div>

<style>
    #right-column {
        height: 1000vw;
        position: relative;
        min-width: 54%;
    }
    .step {
        flex-grow: 3;
        position: absolute;
    }
    .step p {
        margin-bottom: 10px;
    }
    #intro {
        top: 0px;
    }
    #mayor-chart {
        top: 275px;
    }
    #council-chart {
        top: 550px;
    }
    #meeting-type {
        top: 1600px;
    }
    #summer23 {
        top: 1250px;
    }
    #metro-meetings {
        top: 2200px;
    }
    #summer24 {
        top: 3200px;
    }
</style>