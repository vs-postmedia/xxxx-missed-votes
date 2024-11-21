<script>
    export let data = [];

    // COMPONENTS
    import { max } from 'd3-array';
    import { onMount } from 'svelte';
    import CalHeatmap from 'cal-heatmap';
    import 'cal-heatmap/cal-heatmap.css';
    import Tooltip from 'cal-heatmap/plugins/Tooltip';

    // VARS
    let cal, container;

    $: data, paintCal(cal, data)

    function initHeatmap() {
        cal = new CalHeatmap();
        paintCal(cal, data);
    }

    function paintCal(cal, data) {
        if (!cal || data.length < 1) return;

        cal.paint({
            data: {
                source: data,
                x: 'vote_date',
                y: d => +d['n']
            },
            date: {
                start: new Date(data[0].vote_date),
                end: new Date(data[data.length - 1].vote_date)
            },
            domain: {
                dynamicDimension: true,
                label: { position: top },
                padding: [5,5,5,5],
                type: 'month'
            },
            itemSelector: container,
            scale: { 
                color: { 
                    type: 'linear',
                    scheme: 'Blues',
                    domain: [0, 25]
                }
            },
            subDomain: {
                type: 'xDay',
                height: 25,
                width: 25,
                radius: 2,
                label: 'D'
            },
            verticalOrientation: true
        },
        [
            [
            Tooltip,
            {
                text: function (vote_date, n, dayjsDate) {
                return (
                    (n ? `Absent for ${n} votes` : 'No missed votes') + ' on ' + dayjsDate.format('ll')
                );
                },
            },
            ],
        ]
    );
    }

    onMount(initHeatmap);
</script>

<div id="cal-heatmap" bind:this={container}></div>