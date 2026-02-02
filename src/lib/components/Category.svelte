<script>
    import Grid from "$lib/components/Grid.svelte";
    import {onMount} from 'svelte';

    let {data, cwd} = $props();

    function r(start, end) {
        return (Math.random() * (end - start)) + start;
    }

    const h = r(0, 360);
    const s = r(35, 100);
    const v = r(50, 75);

    const mainColor = `hsl(${h}deg ${s}% ${v}%);`;
    const complementaryColor = `hsl(${(h + 180) % 360}deg ${s}% ${v}%);`;

    onMount(() => {
        const sc = Array.from(document.getElementsByClassName("fullscreen-container"))[0];
        sc.style.backgroundColor = mainColor;
    });
</script>

<style>
.fullscreen-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    min-height: 100%;
    overflow: visible;
    box-sizing: border-box;
}

.inner {
    width: 100%;
    height: 100%;
    position: relative;
    overflow-y: auto;
}

@media only screen and (max-width: 500px) {
    .category-header {
        text-align: center;
        padding-bottom: 5%;
    }
}

@media only screen and (min-width: 500px) {
    .category-header {
        padding-top: 2%;
        padding-left: 3.5%;
        padding-bottom: 2%;
    }
}
</style>

<div class="fullscreen-container">
<!-- <body style={`background-color: ${mainColor}`}> -->
<div class="inner" style={`background-color: ${mainColor}`}>
    <h1 class="category-header">{cwd}</h1>

    <!-- definitely a better way to do this other than cwd as a prop -->
    <Grid data={data} cwd={cwd} borderColor={complementaryColor}></Grid>
</div>
<!-- </body> -->
</div>