<script>
    // COMPONENTS
    import { onMount } from 'svelte';
    import { csvParse } from 'd3-dsv';
    import RightColumn from "$components/RightColumn.svelte";
    import CalHeatmap from "$components/CalHeatmap.svelte";
    // import Select from "svelte-select"; // https://github.com/rob-balfre/svelte-select

    

    // DATA
    // import data from "$data/data.js";
    import { menuItems } from "$data/menu-items";
    const dataUrl = 'https://vs-postmedia-data.sfo2.digitaloceanspaces.com/misc/sim-absent-daily.csv';

    // VARIABLES
    let data, value;

    // REACTIVE VARIABLES
    $: value, updateData(value);

    async function fetchData(url) {
        const resp = await fetch(url);
        data = await resp.text();
        return csvParse(data);
    }


    function updateData(value) {
        if (!value || !value.value) return;

        console.log(value);
    }

    async function init() {
        // fetch remote data
        data = await fetchData(dataUrl);
        console.log(data)
    }

    onMount(init);
</script>

<header>
    <h1>VS SvelteKit Template</h1>
    <p class="subhead">Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
</header>

<main> 
    <div id="chart-container"> 
        <CalHeatmap 
            data={data}
        />
        <RightColumn />
    </div>
</main>

<footer>
    <p class="note">NOTE: tk.</p>
    <p class="source">Source:  <a href="https://opendata.vancouver.ca/explore/dataset/council-voting-records/information/?disjunctive.meeting_type&disjunctive.vote_number&disjunctive.council_member&disjunctive.vote" target="_blank">City of Vancouver</a></p>
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
	header .subhead {
		margin: 0 auto;
		max-width: 525px;
		text-align: center;
	}

    #chart-container {
        display: flex;
        flex-flow: space-between;
    }
</style>
