<script>
    let {data, cwd} = $props();

    import Grid from "$lib/components/Grid.svelte";
    function r(start, end) {
        return (Math.random() * (end - start)) + start;
    }

    const h = r(0, 360);
    const s = r(35, 100);
    const v = r(50, 75);

    const mainColor = `hsl(${h}deg ${s}% ${v}%);`;
    const complementaryColor = `hsl(${(h + 180) % 360}deg ${s}% ${v}%);`;
</script>

<style>
global(body) {
  max-width: none;
  overflow: auto;
}

.inner {
    width: 100%;
    height: 100%;
}
</style>

<!-- <body style={`background-color: ${mainColor}`}> -->
<div class="inner" style={`background-color: ${mainColor}`}>
    <h1>{cwd}</h1>

    <!-- definitely a better way to do this other than cwd as a prop -->
    <Grid data={data} cwd={cwd} borderColor={complementaryColor}></Grid>
</div>
<!-- </body> -->