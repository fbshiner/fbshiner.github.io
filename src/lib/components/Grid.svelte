<script>
    import Page from "../../routes/+page.svelte";

    let {data, cwd, borderColor} = $props();
    // import { data } from "$lib/components/data.js"

    let setBrightness = (id, brightness) => {
        document.getElementById(id).style.filter = `brightness(${brightness}%)`
    };

    // have to do this because import.meta.glob only accepts string literals
    let modules = $state(null);
    switch(cwd){
        case "knitting":
            modules = import.meta.glob("$lib/assets/knitting/*.{png,jpeg,jpg}", {
                eager: true,
                import: 'default'
            });
            break;
        case "music":
            modules = import.meta.glob("$lib/assets/music/*.{png,jpeg,jpg}", {
                eager: true,
                import: 'default'
            });
            break;
        case "spinning":
            modules = import.meta.glob("$lib/assets/spinning/*.{png,jpeg,jpg}", {
                eager: true,
                import: 'default'
            });
            break;
        case "misc":
            modules = import.meta.glob("$lib/assets/misc/*.{png,jpeg,jpg}", {
                eager: true,
                import: 'default'
            });
            break;
    }
</script>

<style>
    .grid {
        width: 100%;
        display: flex;
        align-content: stretch;
        flex-wrap: wrap;
        align-items: center;
    }

    .grid img {
        border: 3px solid;
    }

    .cell {
        text-align: center;
        flex: 1;
        padding-bottom: 5%;
    }

    img {
        filter: brightness(100%);
    }

    img:hover {
        cursor: pointer;
        filter: brightness(50%);
        transition: ease 0.3s all;
    }

    @media only screen and (max-width: 500px) {
        .cell {
            max-width: 90%;
            height: auto;
            margin: 0 auto;
            padding-bottom: 5%;
            /* overflow: hidden; */
        }

        img {
            max-width: 90vw;
        }
    }

</style>

<div class="grid">
    <!-- svelte-ignore a11y_no_static_element_interactions --> 
    <!-- do an image glob here too . . . . and send that glob as a parameter to the entry / slug page ideally!!! -->

    <!-- {#each imageUrls as imageUrl}
        <img src={imageUrl} alt="Test"/>
    {/each} -->


    {#each data.summaries as {slug, title, src}}
        <div class="cell" id={title} style="filter: brightness(100%);" onmouseenter={()=> {
            // setBrightness(title, 50);
        }}
        onmouseleave={()=>{
            // ssetBrightness(title, 100);
        }}>            
        <!-- todo: make this routing dynamic depending on subfolder -->
        <!-- use enhanced:img here and pass as a param like in Entry/(knitting/[slug])? -->
        {#if cwd === "knitting"}
            <a href="./{cwd}/{slug}"><img src={modules[`/src/lib/assets/knitting/${src.split(".")[0]}.${src.split(".")[1]}`]} alt="test" style={`border: 3px solid ${borderColor}`}/></a>
        {:else if cwd === "music"}
            <a href="./{cwd}/{slug}"><img src={modules[`/src/lib/assets/music/${src.split(".")[0]}.${src.split(".")[1]}`]} alt="test" style={`border: 3px solid ${borderColor}`}/></a>
        {:else if cwd === "spinning"}
            <a href="./{cwd}/{slug}"><img src={modules[`/src/lib/assets/spinning/${src.split(".")[0]}.${src.split(".")[1]}`]} alt="test" style={`border: 3px solid ${borderColor}`}/></a>
        {:else if cwd === "misc"}
            <a href="./{cwd}/{slug}"><img src={modules[`/src/lib/assets/misc/${src.split(".")[0]}.${src.split(".")[1]}`]} alt="test" style={`border: 3px solid ${borderColor}`}/></a>
        {/if}
        <br>
            {title}
        </div>
    {/each}
</div>