<script>
    export let data = [];

    // COMPONENTS
    import { max } from 'd3-array';
    import { onMount } from 'svelte';
    import CalHeatmap from 'cal-heatmap';
    import 'cal-heatmap/cal-heatmap.css';
    import Legend from 'cal-heatmap/plugins/Legend';
    import Tooltip from 'cal-heatmap/plugins/Tooltip';

    // VARS
    let cal, container;
    const legendContainer = '#legend';
    const legendLabel = 'Sim’s daily absent votes';

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
                    height: 40,
                    offset: {
                        x: 0,
                        y: -20
                    },
                    position: top,
                    text: 'MMM YYYY',
                    textAlign: 'left'
                },
                padding: [10,5,20,5],
                type: 'month'
            },
            itemSelector: container,
            range: 25,
            scale: { 
                color: { 
                    // type: 'linear',
                    type: 'quantile',
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
                Legend,
                {
                    itemSelector: legendContainer,
                    label: legendLabel
                },
            ],
            [
                Tooltip,
                {
                    text: function (vote_date, n, dayjsDate) {
                        const voteLabel = n > 1 ? 'votes' : 'vote';
                        const text = (n ? `Sim missed ${n} ${voteLabel}` : 'No missed votes') + ' on ' + dayjsDate.format('ll')
                        
                        return text;
                    },
                },
            ],
        ]
    );
    }

    // kick isht off!!!
    onMount(initHeatmap);
</script>

<div id="cal-heatmap" bind:this={container}></div>

<style>
    #cal-heatmap {
        margin-left: 25px;
        margin-top: 15px;
        max-width: 160px;
    }
    #ch-tooltip {
        font-size: 1rem !important;
    }
    #ch-tooltip #ch-tooltip-body {
        color: #FFF;
        font-size: 1rem !important;
    }

    @media screen and (min-width: 450px) {
        #cal-heatmap {
           max-width: none;
        }
    }
</style>