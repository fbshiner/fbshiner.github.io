<script>
    import Entry from "$lib/components/Entry.svelte";
    
    let {data} = $props();

    const images = import.meta.glob("$lib/assets/misc/*.{png,jpeg,jpg}", {
        eager: true,
        import: 'default'
    });

    const title = data.post.title;
    const description = data.post.description;

    const srcInfo = data.post.src.split(".");
    const path = `/src/lib/assets/misc/${srcInfo[0]}.${srcInfo[1]}`;
    const altText = data.post.alt;

    const link = data.post.link;
    const linkText = data.post.linkText;
    
    const pageContext = {
        "image": images[path],
        "title": title,
        "description": description,
        "alt": altText,
        "link": link,
        "linkText": linkText,
    }
</script>
<!-- description and image of proj -->
<Entry PageContext={pageContext}></Entry>