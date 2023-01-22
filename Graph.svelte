<script>
    export let todo_count = [];
    let y_points = [];
    let points = '';
    let max_count = 0;
    let y_scale = 0;
    $: {
        points = '';
        max_count = Math.max(...todo_count);
        y_scale = 200/(Math.max(max_count, 1));
        todo_count.forEach(function (c, i) {
            points = points + i*20;
            points = points + ',';
            points = points + (100-c*y_scale);
            points = points + ' ';
        });
        if (todo_count.length > 20) {
            todo_count.shift();
        }
        y_points = [Math.round(0), 
            // Math.round(max_count * 0.25), 
            Math.round(max_count * 0.5), 
            // Math.round(max_count * 0.75), 
            Math.round(max_count)
        ];
    };

</script>

<svg width="400" height="100">
	<!-- x axis -->
	<line x1="0" x2="400" y1="100" y2="100"></line>
	<g class="x" transform="translate(0,120)">
		<text x="0">0</text>
		<text x="100">5</text>
		<text x="200">10</text>
		<text x="300">15</text>
		<text x="400">20</text>
	</g>
	
	<!-- y axis -->
	<line x1="0" x2="0" y1="-100" y2="100"></line>
	<g class="y" transform="translate(-10,0)">
        {#each y_points as c}
            <text y="{100-c*y_scale}">{c}</text>
        {/each}
	</g>
	
	<!-- data -->
	<polyline style="stroke: #3f4252; stroke-width: 2" points={points}></polyline>

</svg>

<style>
	svg {
		overflow: visible;
		margin-top: 150px;
	}
	
	line, polyline {
		fill: none;
		stroke: var(--color-text);
	}
	
	.x text {
		text-anchor: middle;
	}
	
	.y text {
		text-anchor: end;
		dominant-baseline: middle;
	}
</style>