<script>
    import Grid from "$lib/components/Grid.svelte";
    import {onMount} from 'svelte';
    import knittingSvg from "$lib/assets/svgs/knitting.svg";
    import spinningSvg from "$lib/assets/svgs/spinning.svg";
    import musicSvg from "$lib/assets/svgs/music.svg";
    import miscSvg from "$lib/assets/svgs/misc.svg";


    let {data, cwd} = $props();

    function r(start, end) {
        return (Math.random() * (end - start)) + start;
    }

    // from https://stackoverflow.com/questions/36721830/convert-hsl-to-rgb-and-hex
    function hslToHex(h, s, l) {
        l /= 100;
        const a = s * Math.min(l, 1 - l) / 100;
        const f = n => {
            const k = (n + h / 30) % 12;
            const color = l - a * Math.max(Math.min(k - 3, 9 - k, 1), -1);
            return Math.round(255 * color).toString(16).padStart(2, '0');   // convert to Hex and prefix "0" if needed
        };
        return `#${f(0)}${f(8)}${f(4)}`;
    }

    const h = r(0, 360);
    const c = (h + 180) % 360;
    const s = r(35, 100);
    const v = r(50, 75);

    const mainColor = `hsl(${h}deg ${s}% ${v}%);`;
    const complementaryColor = `hsl(${c}deg ${s}% ${v}%);`;

    let svg;
    switch (cwd) {
        case "knitting":
            svg = `<svg fill="${hslToHex(c,s,v)}" height="200px" width="200px" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 512 512" xml:space="preserve">
            <path d="M457.596,359.689c30.698-38.077,49.138-86.397,49.138-138.822c0-75.203-37.93-141.968-95.594-182.141 c-0.488-0.49-1.044-0.94-1.686-1.326c-0.316-0.189-0.637-0.354-0.96-0.506c-27.191-18.368-58.625-30.866-92.448-35.677 c-0.526-0.121-1.053-0.195-1.576-0.222C304.779-0.312,294.9-1,284.867-1C222.096-1,165.2,25.422,124.741,67.689 c-1.138,0.702-2.049,1.675-2.685,2.868C85.45,110.16,63,163.015,63,220.867c0,48.593,15.845,93.658,42.606,130.311 C104.44,373.959,86.117,391.533,63,391.533c-33.28,0-59.733,26.453-59.733,59.733C3.267,484.547,29.72,511,63,511 c33.28,0,59.733-26.453,59.733-59.733c0-5.12-3.413-8.533-8.533-8.533c-5.12,0-8.533,3.413-8.533,8.533 c0,23.893-18.773,42.667-42.667,42.667c-23.893,0-42.667-18.773-42.667-42.667c0-23.893,18.773-42.667,42.667-42.667 c26.424,0,48.528-16.684,56.521-40.213c40.707,45.55,99.823,74.347,165.346,74.347c67.598,0,128.376-30.649,169.156-78.724 C455.717,363.084,456.956,361.594,457.596,359.689z M83.049,255.611c-1.952-11.301-2.982-22.908-2.982-34.744 c0-10.689,0.834-21.193,2.433-31.452c5.53,8.065,13.535,16.109,24.021,23.772c49.493,36.693,139.093,64.853,239.787,64.853 c45.436,0,93.267-5.621,139.63-18.366c-6.389,32.962-20.743,63.169-40.969,88.518C243.649,356.078,131.549,327.149,83.049,255.611 z M488.601,241.757c-0.79,0.001-1.583,0.137-2.348,0.443c-93.867,26.453-271.36,31.573-369.493-42.667 c-17.067-12.8-26.453-26.453-26.453-36.693c0-1.346-0.242-2.571-0.683-3.65c7.695-24.184,19.784-46.453,35.316-65.866 c5.165,12.359,15.292,24.611,29.443,35.812c0.761,0.959,1.749,1.708,2.915,2.219c21.703,16.054,51.815,29.681,88.295,38.531 c1.382,0.953,3.126,1.487,5.14,1.487c0.398,0,0.791-0.012,1.187-0.016c26.78,5.971,56.786,9.403,89.266,9.403 c42.667,0,90.453-5.973,139.093-20.48c0.057-0.011,0.111-0.032,0.168-0.045c5.988,19.18,9.219,39.547,9.219,60.632 C489.667,227.916,489.305,234.886,488.601,241.757z M392.834,47.064c-35.474,53.412-79.032,106.094-140.116,107.215 c-25.804-5.976-48.24-14.458-66.459-24.542c58.609-11.296,99.689-61.111,132.352-110.854 C345.448,23.38,370.556,33.141,392.834,47.064z M474.766,144.415c-64.627,18.298-124.87,22.442-176.196,17.329 c44.981-18.671,79.545-61.773,108.499-104.949C436.938,79.132,460.562,109.408,474.766,144.415z M284.867,16.067 c4.88,0,9.719,0.184,14.516,0.525c-45.479,67.226-86.486,97.293-135.364,98.425c-15.163-12.053-24.315-24.708-25.727-36.809 C175.558,39.934,227.556,16.067,284.867,16.067z M93.727,294.187c53.719,49.429,146.984,72.599,292.686,72.599 c14.058,0,28.129-0.405,42.738-0.933c-37.091,36.915-88.142,59.813-144.285,59.813 C198.031,425.667,123.379,370.889,93.727,294.187z">
            </path></svg>`
            break;
        case "music":
            svg = `<svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M10.0909 11.9629L19.3636 8.63087V14.1707C18.8126 13.8538 18.1574 13.67 17.4545 13.67C15.4964 13.67 13.9091 15.096 13.9091 16.855C13.9091 18.614 15.4964 20.04 17.4545 20.04C19.4126 20.04 21 18.614 21 16.855C21 16.855 21 16.8551 21 16.855L21 7.49236C21 6.37238 21 5.4331 20.9123 4.68472C20.8999 4.57895 20.8852 4.4738 20.869 4.37569C20.7845 3.86441 20.6352 3.38745 20.347 2.98917C20.2028 2.79002 20.024 2.61055 19.8012 2.45628C19.7594 2.42736 19.716 2.39932 19.6711 2.3722L19.6621 2.36679C18.8906 1.90553 18.0233 1.93852 17.1298 2.14305C16.2657 2.34086 15.1944 2.74368 13.8808 3.23763L11.5963 4.09656C10.9806 4.32806 10.4589 4.52419 10.0494 4.72734C9.61376 4.94348 9.23849 5.1984 8.95707 5.57828C8.67564 5.95817 8.55876 6.36756 8.50501 6.81203C8.4545 7.22978 8.45452 7.7378 8.45455 8.33743V16.1307C7.90347 15.8138 7.24835 15.63 6.54545 15.63C4.58735 15.63 3 17.056 3 18.815C3 20.574 4.58735 22 6.54545 22C8.50355 22 10.0909 20.574 10.0909 18.815C10.0909 18.815 10.0909 18.8151 10.0909 18.815L10.0909 11.9629Z" fill="${hslToHex(c,s,v)}">
            </path></svg>`;
            break;
        case "spinning":
            svg = `<svg viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 10V3M13.4141 10.5857L18.3639 5.63599M14 12H21M13.4143 13.4141L18.364 18.3639M12 14V21M10.5859 13.4143L5.63611 18.364M10 12H3M10.5857 10.5859L5.63599 5.63611M21 12C21 16.9706 16.9706 21 12 21C7.02944 21 3 16.9706 3 12C3 7.02944 7.02944 3 12 3C16.9706 3 21 7.02944 21 12ZM14 12C14 13.1046 13.1046 14 12 14C10.8954 14 10 13.1046 10 12C10 10.8954 10.8954 10 12 10C13.1046 10 14 10.8954 14 12Z" stroke="${hslToHex(c,s,v)}" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            </path></svg>`;
            break;
        case "misc":
            svg = miscSvg;
            break;
    }

    // encoding from https://www.tutorialpedia.org/blog/drawing-an-svg-file-on-a-html5-canvas/#default-methods-to-draw-svg-on-html5-canvas
    const encodedSvg = encodeURIComponent(svg);
    const svgDataUrl = `data:image/svg+xml;charset=utf-8,${encodedSvg}`; 

    onMount(() => {
        const sc = Array.from(document.getElementsByClassName("fullscreen-container"))[0];
        sc.style.backgroundColor = mainColor;

        const canvas = document.getElementById("svg-canvas");
        const ctx = canvas.getContext("2d");

        const WIDTH = canvas.width;
        const HEIGHT = canvas.height;
        const BACKGROUND = "#4bad62";
        const FOREGROUND = "#c9feff";
        const STROKE_WIDTH = 8;
        const RADIUS = Math.min(WIDTH, HEIGHT);

        function clear() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        }

        const FPS = 10;

        // ctx.fillStyle = FOREGROUND;
        // ctx.strokeStyle = FOREGROUND;
        // ctx.lineWidth = STROKE_WIDTH;
        
        let i = 0;
        const totalSteps = 200;
        
        const NUM_SHAPES = 20;
        const shapes = [];
        const JITTER_RANGE = 2;
        const PLACEMENT_RANGE = 20;

        for (let i = 0; i < NUM_SHAPES; i++) {
            const length = Math.random() * 75 + 25;
            const scale_factor = i/NUM_SHAPES;
            const x = (scale_factor*(WIDTH-PLACEMENT_RANGE)) + Math.random() * PLACEMENT_RANGE;
            const y = Math.random() * HEIGHT;
            // const x = Math.random() * (WIDTH);
            // const y = Math.random() * (HEIGHT);
            // const x = ((WIDTH-PLACEMENT_RANGE)/i) // space this out properly

            // console.log(x, y, length);
            shapes.push({
                "xVal": x,
                "yVal": y,
                "length": length,
            });
        }
        // console.log(shapes);

        function frame() {
            console.log(shapes);
            clear();

            // IDEA: Draw multiple svg, don't scale but just have them jitter in place
            const scale = i/totalSteps;
            shapes.forEach((shape) => {
                const xJitter = Math.random() * JITTER_RANGE - (JITTER_RANGE/2);
                const yJitter = Math.random() * JITTER_RANGE - (JITTER_RANGE/2);
                ctx.drawImage(img, shape.xVal, shape.yVal, shape.length + xJitter, shape.length + yJitter);
            });

            // ctx.drawImage(img, 0, 0, i, i);
            // randomize 0,0 set i,i to CONSTANT + random(-RANGE, RANGE), CONSTANT + random(-RANGE, RANGE)
            i = (i+1)%totalSteps;

            setTimeout(frame, 1000/FPS);
        }

        const img = new Image();

        img.onload = () => {
            // console.log("Drawing......");
            // ctx.drawImage(img, 0, 0, 200, 200);
            setTimeout(frame, 1000/FPS);
        };

        img.onerror = (error) => {
            console.error("Failed to load svg: ", error);
        };

        img.src = svgDataUrl;
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

#svg-canvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    min-height: 100%;
    overflow: visible;
    box-sizing: border-box;  
}

@media only screen and (max-width: 500px) {
    .category-header {
        text-align: center;
        padding-bottom: 5%;
    }
}

@media only screen and (min-width: 500px) {
    .category-header {
        text-align: left;
        padding-bottom: 2%;
    }
}
</style>

<div class="fullscreen-container">
<!-- <body style={`background-color: ${mainColor}`}> -->
<div class="inner" style={`background-color: ${mainColor}`}>
    <h1 class="category-header">{cwd}</h1>
    <canvas id="svg-canvas">

    </canvas>

    <!-- definitely a better way to do this other than cwd as a prop -->
    <Grid data={data} cwd={cwd} borderColor={complementaryColor}></Grid>
</div>
<!-- </body> -->
</div>