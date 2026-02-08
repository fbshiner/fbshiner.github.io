<script>
    import Entry from "$lib/components/Entry.svelte";
    
    let {data} = $props();

    const images = import.meta.glob("$lib/assets/music/*.{png,jpeg,jpg}", {
        eager: true,
        import: 'default'
    });

    const musicFiles = import.meta.glob("$lib/assets/music/*.{mp3,wav,ogg,flac}", {
        eager: true,
        import: 'default'
    });

    const title = data.post.title;
    const description = data.post.description;
    const link = data.post.link;
    const linkText = data.post.linkText;

    const srcInfo = data.post.src.split(".");
    const path = `/src/lib/assets/music/${srcInfo[0]}.${srcInfo[1]}`;

    const musicInfo = data.post.musicFile.split(".");
    const musicPath = `/src/lib/assets/music/${musicInfo[0]}.${musicInfo[1]}`;

    const pageContext = {
        "image": images[path],
        "title": title,
        "description": description,
        "link": link,
        "linkText": linkText,
        "musicFile": musicFiles[musicPath],
    }
    
</script>
<!-- description and image of proj -->
<Entry PageContext={pageContext}></Entry>