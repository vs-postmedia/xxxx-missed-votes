<script>
    // COMPONENTS
    import { onMount } from 'svelte';
    import { csvParse } from 'd3-dsv';
    import RightColumn from "$components/RightColumn.svelte";
    import CalHeatmap from "$components/CalHeatmap.svelte";

    

    // DATA
    const dataUrl = 'https://vs-postmedia-data.sfo2.digitaloceanspaces.com/misc/sim-absent-daily.csv';

    // VARIABLES
    let data;

    async function fetchData(url) {
        const resp = await fetch(url);
        data = await resp.text();
        return csvParse(data);
    }

    async function init() {
        // fetch remote data
        data = await fetchData(dataUrl);
        console.log(data)
    }

    onMount(init);
</script>

<header>
    <h1>Where’s the Mayor?</h1>
    <!-- <p class="subhead">Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p> -->
</header>

<main> 
    <div id="chart-container"> 
        <RightColumn />
        <CalHeatmap 
            data={data}
        />
    </div>
</main>

<footer>
    <p class="note">NOTE: Voting record data as of Nov. 19, 2024, unless otherwise noted.</p>
    <div class="bottom-row">
        <p class="source">Source:  <a href="https://opendata.vancouver.ca/explore/dataset/council-voting-records/information/?disjunctive.meeting_type&disjunctive.vote_number&disjunctive.council_member&disjunctive.vote" target="_blank">City of Vancouver</a></p>
        <div style='width:100%!;margin-top:4px!important;text-align:right!important;'><a class='flourish-credit' href='https://public.flourish.studio/visualisation/20405301/?utm_source=embed&utm_campaign=visualisation/20405301' target='_top' style='text-decoration:none!important'><img alt='Made with Flourish' src='https://public.flourish.studio/resources/made_with_flourish.svg' style='width:105px!important;height:16px!important;border:none!important;margin:0!important;'></a></div>
    </div>
</footer>
  
<style>
    @import '$css/normalize.css';
    @import '$css/fonts.css';
    @import '$css/colors.css';
    @import '$css/app.css';

    header {
		margin-bottom: 2rem;
	}
	header > h1 {
		text-align: center;
	}
    footer .bottom-row {
        display: flex;
        justify-content: space-between;
    }

    #chart-container {
        display: flex;
        flex-flow: space-between;
    }
</style>
