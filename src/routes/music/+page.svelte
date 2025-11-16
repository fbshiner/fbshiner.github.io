<script>
    let {data} = $props();
    import Category from "$lib/components/Category.svelte"
</script>

<Category data={data} cwd="music"></Category>