<script>
    import Image from "$lib/components/Image.svelte";
    import {onMount} from 'svelte';
    // access all images in directory, put in an array, pick a random (10-20) amount of photos from the entire directory
    const imageModules = import.meta.glob("../lib/assets/ravelry/*.{png,jpeg,jpg}", {
        eager: true,
        query: '?url', 
        import: 'default'
    });

    const imageUrls = Object.values(imageModules);
    // .slice(0,  50);
    
    let index = 0;

    const indices = [0, 1]; // maybe try [0, 1]
</script>

<style>
    .fullscreen-container {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        max-height: 100%;
        background-color: #a52a2a;
        overflow: hidden;
        box-sizing: border-box;
    }

    h1 {
        text-align: center;
    }

    .navbar {
        padding-top: 0.5%;
        padding-bottom: 0.5%;
        background-color: #a52a2a;
        text-align: center;
    }

    .navbar a {
        padding-left: 5%;
        padding-right: 5%;
        font-size: larger;
        color: #000;
        transform: scale(1.0);
        transition: all 0.8s ease 
    }

    .navbar a:hover {
        transform: scale(1.1);
        transition: all 0.8s ease 
    }

    .flex-container {
        display: flex;
        width: 100%;
        flex-wrap: wrap;
        /* align-content: flex-start; */
        align-content: stretch;
        justify-content: space-evenly;
        max-height: 100%;
        overflow: hidden;

    }

    .page {
        background-color: brown;
        /* width: 100%;
        height: 100%; */
        /* height: 100vh; */
    }

</style>

<div class="fullscreen-container">
<div class="navbar">
    <a href="./knitting">knitting</a>
    <a href="./music">music</a>
    <a href="./spinning">spinning</a>
    <a href="./misc">misc</a>
</div>

<div class="page">
    <h1> FRANKIES WORLD </h1>

    <div class="welcome" style="text-align: center;">
        <h2>welcome :)</h2>
    </div>

    <!-- TODO: make each image get bigger when you hover over them? Use grid.svelte for example -->
    <!-- <Image src="src/lib/assets/ravelry/poppop_dagrun_luggar.jpg" alt="test"></Image> -->
    <div class="flex-container">
        {#each indices as index} 
            {#each imageUrls as imageUrl}
                <Image src={imageUrl} alt="Test"></Image>
            {/each}
        {/each}
    </div>
</div>
</div>