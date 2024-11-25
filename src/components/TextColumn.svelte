<script>
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
        <p>Mayor Ken Sim has been marked absent on city council votes far more often than previous mayors.</p>
        <p>The calendar to the right shows how many votes Sim missed on any given day since he was elected. Hover or tap a day to see how many times the mayor was marked “Absent.”</p>
    </div>
    <div id="legend" class="step"></div>
    <div id="mayor-chart" class="step">
        <iframe src='https://flo.uri.sh/visualisation/20404697/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='max-width:200px;height:150px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe>
    </div>
    <div id="council-chart" class="step">
        <p>The mayor missed more votes than his colleagues...</p>
        <iframe src='https://flo.uri.sh/visualisation/20404954/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='max-width:200px;height:350px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe>
    </div>
    <div id="summer23" class="step">
        <p>...and in the summer of 2023 he missed seven days of council meetings, totalling 81 votes – 43 of them for attending the three-day Collision tech conference, which Vancouver will host in 2025.</p>
    </div>
    <div id="meeting-type" class="step">
        <p>The mayor is most likely to skip public hearings, which are often held in the evening.</p>
        <iframe src='https://flo.uri.sh/visualisation/20405084/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='max-width:180px;height:250px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe>
    </div>
    <div id="metro-meetings" class="step">
        <p>He isn’t just skipping council meetings. He’s only attended a quarter of the 41 Metro Vancouver committee and board meetings.</p>
        <iframe src='https://flo.uri.sh/visualisation/20405301/embed' title='Interactive or visual content' class='flourish-embed-iframe' frameborder='0' scrolling='no' style='max-width:180px;height:150px;' sandbox='allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation'></iframe>
    </div>
    <div id="summer24" class="step">
        <p>Sim missed 114 votes in the summer of 2024, many of which were connected to his attendance at two tech conferences: Collision in Toronto and London Tech Week.</p>
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
    #legend {
        top: 200px;
    }
    #mayor-chart {
        top: 350px;
    }
    #council-chart {
        top: 700px;
    }
    #summer23 {
        top: 1450px;
    }
    #meeting-type {
        top: 2000px;
    }
    #metro-meetings {
        top: 3000px;
    }
    #summer24 {
        top: 3800px;
    }
</style>