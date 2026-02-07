<script>
    // the way to go about this is, in your given display grid, you get the import 
    let { PageContext } = $props();
    // console.log(PageContext);

    // const imageRightAlign = Math.random() > 0.5;
    const imageAlign = Math.random() > 0.5;
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
    h1 {
        text-align: center;
    }

    /* ========================================================================================================== */
    @media only screen and (max-width: 500px) {
        h1 {
            padding-bottom: 2%;
        }
        
        .image-and-description {
            width: 100%;

            display: grid;
            grid-template-columns: auto;
            grid-template-rows: 1fr 1fr;
            align-items: center;
            text-align: center;
        }

        img {
            max-width: 100%;
            height: auto;
        }
    }

    @media only screen and (min-width: 500px) {
        .image-and-description {
            width: 100%;

            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-template-rows: auto;
            align-items: center;
            text-align: center;
        }

        .entry-imageLeftAlign {
            order: 0;
        }

        .entry-imageRightAlign {
            order: 1;
        }   

        .entry-textLeftAlign {
            order: 0;
        }

        .entry-textRightAlign {
            order: 1;
        }

        img {
            max-width: 100%;
            height: auto;
        }
    }

    .fullscreen-container {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        box-sizing: border-box;
    }

    .entry-page {
        width: 90%;
        height: 100%;
        margin: 0 auto;

        display: grid;
        grid-template-rows: 1fr 6fr 3fr;
        grid-template-columns: auto;
    }

    .entry-header {
        width: 100%;
        text-align: center;
    }

    .link-and-player {
        width: 100%;

        display: grid;
        grid-template-rows: 1fr 1fr;
        grid-template-columns: auto;
        text-align: center;
        align-items: flex-start;
    }

    audio {
        filter: sepia(20%) saturate(70%) grayscale(1) contrast(99%) invert(12%);
    }
</style>

<div class="fullscreen-container" style={`background-color:${mainColor}`}>
    <div class="entry-page">
        <div class="entry-header">
            <h1>{PageContext.title}</h1>
        </div>

        <div class="image-and-description">
            <div class={["entry-image", (imageAlign? "entry-imageRightAlign": "entry-imageLeftAlign")]}>
                <img src={PageContext.image} style={`border: solid ${r(3, 10)}px ${complementaryColor};`} alt={PageContext.title}/>
            </div>
            
            <div class={["entry-description", (imageAlign? "entry-textLeftAlign": "entry-textRightAlign")]}>
                {#if PageContext.description && PageContext.description !== "test"}
                    {PageContext.description}
                {/if}
            </div>
        </div>

        <div class="link-and-player">
            <div class="entry-link">
                {#if PageContext.link}
                    <a href={PageContext.link}>
                        {#if PageContext.linkText}
                            {PageContext.linkText}
                        {:else}
                            Link
                        {/if}

                    </a>
                {/if}
            </div>
            <div class="entry-player">
                {#if PageContext.musicFile}
                    <audio controls>
                        <source src={PageContext.musicFile}>
                    </audio>
                {/if}
            </div>
        </div>
    </div>

</div>

<!-- has slug, title, img_src -- needs desc? -->
<!-- <div style={`height: 100vh; background-color:${mainColor};`}>
  <h1>{PageContext.title}</h1>
<div class="page-container" >

 <div class={["image-container", (imageAlign? "imageRightAlign": "imageLeftAlign")]}>
    <img src={PageContext.image} style={`border: solid ${r(3, 10)}px ${complementaryColor};`} alt="Placeholder"/>
 </div>

<div class={["text-container", (imageAlign? "textLeftAlign" : "textRightAlign")]}>
    {#if PageContext.description && PageContext.description !== "test"}
        {PageContext.description}
    {/if}

    {#if PageContext.link}
        <a href={PageContext.link}>
            {#if PageContext.linkText}
                {PageContext.linkText}
            {:else}
                Link
            {/if}

        </a>
    {/if}
</div>

</div>
</div> -->