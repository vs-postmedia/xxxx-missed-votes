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

    $: data, paintCal(cal, data);

    function initHeatmap() {
        cal = new CalHeatmap();
        paintCal(cal, data);
    }

    function paintCal(cal, data) {
        if (!cal || data.length < 1) return;

        const domainMax = max(data, d => +d.n);

        cal.paint({
            data: {
                source: data,
                x: 'vote_date',
                y: d => +d['n']
            },
            date: {
                start: new Date(data[0].vote_date),
                end: new Date('2024-11-05')
                // end: new Date(data[data.length - 1].vote_date)
            },
            domain: {
                dynamicDimension: true,
                label: { 
                    offset: {
                        x: 0,
                        y: -20
                    },
                    position: top,
                    text: 'MMM YYYY',
                    textAlign: 'left'
                },
                padding: [5,5,5,5],
                type: 'month'
            },
            itemSelector: container,
            range: 25,
            scale: { 
                color: { 
                    type: 'linear',
                    scheme: 'Blues',
                    domain: [0, domainMax]
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
                    (n ? `Sim missed ${n} votes` : 'No missed votes') + ' on ' + dayjsDate.format('ll')
                );
                },
            },
            ],
        ]
    );
    }

    onMount(() => {

        initHeatmap()
    });
</script>

<div id="cal-heatmap" bind:this={container}></div>

<style>
    #cal-heatmap {
        /* position: absolute; */
        /* margin: 0 auto; */
        width: 200px;
    }
    #app .ch-domain-text {
        font-size: 1.05rem !important;
    }
</style>