<script>
    import { onMount } from "svelte";

    let {data} = $props();
    // import Category from "$lib/components/Category.svelte"
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

    let svg = `<svg fill="${hslToHex(c,s,v)}" height="200px" width="200px" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg"
     xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 512 512" xml:space="preserve"><g id="SVGRepo_bgCarrier" 
     stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier">
     <g> <g> <path d="M232.389,171.905c-5.603-5.603-13.051-8.688-20.974-8.688c-7.923,0-15.372,3.085-20.973,8.688 c-5.604,5.603-8.689,13.052-8.689,20.975c0,7.923,3.085,15.373,8.688,20.974c5.603,5.603,13.051,8.688,20.974,8.688 c7.923,0,15.372-3.085,20.975-8.688C243.955,202.288,243.955,183.471,232.389,171.905z M221.172,202.636 c-2.606,2.605-6.071,4.04-9.757,4.04c-3.686,0-7.15-1.434-9.756-4.04s-4.04-6.071-4.04-9.756s1.434-7.15,4.04-9.756h0.001 c2.605-2.606,6.07-4.04,9.755-4.04s7.151,1.435,9.756,4.04C226.55,188.503,226.55,197.257,221.172,202.636z"></path> </g> </g> <g> <g> <path d="M342.739,61.555c-11.564-11.566-30.384-11.566-41.949,0h-0.001c-11.565,11.566-11.565,30.384,0.001,41.95 c5.782,5.784,13.378,8.674,20.974,8.674s15.192-2.891,20.974-8.674c5.604-5.602,8.689-13.051,8.689-20.974 C351.428,74.606,348.342,67.156,342.739,61.555z M331.521,92.286c-5.381,5.378-14.134,5.38-19.513,0 c-5.38-5.38-5.38-14.133,0-19.513c5.381-5.378,14.132-5.378,19.513,0c2.606,2.606,4.04,6.071,4.04,9.756 S334.127,89.68,331.521,92.286z"></path> </g> </g> <g> <g> <path d="M342.739,282.255c-11.564-11.566-30.384-11.566-41.949,0h-0.001c-11.565,11.565-11.565,30.384,0.001,41.95 c5.782,5.784,13.378,8.674,20.974,8.674s15.192-2.891,20.975-8.674c5.603-5.603,8.688-13.052,8.688-20.975 C351.428,295.306,348.342,287.856,342.739,282.255z M331.521,312.986c-5.381,5.378-14.132,5.377-19.513,0 c-5.38-5.38-5.38-14.133,0-19.513c5.381-5.378,14.132-5.378,19.513,0c2.606,2.606,4.04,6.071,4.04,9.756 S334.126,310.38,331.521,312.986z"></path> </g> </g> <g> <g> <path d="M453.089,171.905c-5.603-5.603-13.051-8.688-20.974-8.688c-7.923,0-15.372,3.085-20.973,8.688 c-5.604,5.603-8.689,13.052-8.689,20.975c0,7.923,3.085,15.373,8.688,20.974c5.603,5.603,13.051,8.688,20.974,8.688 c7.923,0,15.372-3.085,20.976-8.688C464.655,202.288,464.655,183.471,453.089,171.905z M441.872,202.636 c-2.606,2.605-6.071,4.04-9.757,4.04s-7.15-1.434-9.756-4.04c-2.606-2.606-4.04-6.071-4.04-9.756s1.434-7.15,4.04-9.756h0.001 c2.605-2.606,6.07-4.04,9.755-4.04c3.685,0,7.151,1.435,9.756,4.04C447.25,188.503,447.25,197.257,441.872,202.636z"></path> </g> </g> <g> <g> <path d="M144.069,335.625c-16.356,0-29.662,13.307-29.662,29.662s13.306,29.662,29.662,29.662s29.664-13.306,29.664-29.662 C173.732,348.932,160.425,335.625,144.069,335.625z M144.069,379.084c-7.607,0-13.797-6.189-13.797-13.797 c0-7.607,6.19-13.797,13.797-13.797c7.608,0,13.798,6.19,13.798,13.797S151.677,379.084,144.069,379.084z"></path> </g> </g> <g> <g> <path d="M66.04,257.595c-16.356,0-29.664,13.306-29.664,29.662c0,16.355,13.307,29.662,29.664,29.662 c16.355,0,29.661-13.306,29.662-29.662C95.703,270.902,82.397,257.595,66.04,257.595z M66.04,301.054 c-7.608,0-13.798-6.19-13.798-13.797c0-7.607,6.19-13.797,13.798-13.797c7.607,0,13.796,6.19,13.797,13.797 C79.837,294.865,73.647,301.054,66.04,301.054z"></path> </g> </g> <g> <g> <path d="M222.097,257.595c-16.356,0-29.662,13.306-29.662,29.662c0,16.355,13.306,29.662,29.662,29.662 s29.664-13.306,29.664-29.662C251.761,270.902,238.454,257.595,222.097,257.595z M222.097,301.054 c-7.607,0-13.797-6.19-13.797-13.797c0-7.607,6.19-13.797,13.797-13.797c7.609,0,13.798,6.19,13.798,13.797 C235.895,294.865,229.705,301.054,222.097,301.054z"></path> </g> </g> <g> <g> <path d="M66.04,413.654c-16.356,0-29.664,13.307-29.664,29.662c0,16.355,13.307,29.662,29.664,29.662 c16.355,0,29.662-13.307,29.662-29.662C95.703,426.961,82.397,413.654,66.04,413.654z M66.04,457.112 c-7.608,0-13.798-6.19-13.798-13.797c0-7.607,6.19-13.797,13.798-13.797c7.607,0,13.797,6.19,13.797,13.797 C79.837,450.922,73.647,457.112,66.04,457.112z"></path> </g> </g> <g> <g> <path d="M222.097,413.654c-16.356,0-29.662,13.307-29.662,29.662c0,16.355,13.306,29.662,29.662,29.662 s29.664-13.307,29.664-29.662C251.761,426.961,238.454,413.654,222.097,413.654z M222.097,457.112 c-7.607,0-13.797-6.19-13.797-13.797c0-7.607,6.19-13.797,13.797-13.797c7.609,0,13.798,6.19,13.798,13.797 C235.895,450.922,229.705,457.112,222.097,457.112z"></path> </g> </g> <g> <g> <path d="M502.449,169.82L344.824,12.196c-6.159-6.16-14.35-9.552-23.06-9.552c-8.711,0-16.901,3.392-23.06,9.551L141.081,169.82 c-6.16,6.159-9.552,14.349-9.552,23.06c0.001,8.711,3.393,16.901,9.552,23.06l5.277,5.277H32.612 C14.63,221.217,0,235.847,0,253.83v222.914c0,17.982,14.63,32.612,32.612,32.612h222.914c17.982,0,32.611-14.63,32.611-32.612 V362.997l10.567,10.567c6.158,6.159,14.348,9.551,23.059,9.552c0.001,0,0.002,0,0.003,0c8.709,0,16.899-3.392,23.059-9.552 L502.448,215.94c6.16-6.159,9.552-14.349,9.552-23.06S508.608,175.98,502.449,169.82z M272.272,476.743L272.272,476.743 c0,9.234-7.513,16.747-16.746,16.747H32.612c-9.234,0-16.747-7.513-16.747-16.747V253.83c0-9.234,7.513-16.747,16.747-16.747 h222.914c9.233,0,16.746,7.513,16.746,16.747V476.743z M491.23,204.722L333.606,362.345c-3.164,3.164-7.368,4.905-11.84,4.905 h-0.001c-4.474,0-8.68-1.742-11.841-4.905l-21.786-21.785V253.83c0-16.859-12.859-30.771-29.283-32.444 c-1.095-0.111-2.205-0.168-3.33-0.168h-86.731l-16.496-16.496c-3.163-3.164-4.906-7.369-4.906-11.842s1.741-8.679,4.906-11.841 L309.924,23.415c3.161-3.163,7.367-4.905,11.84-4.905c4.473,0,8.678,1.742,11.841,4.905l157.623,157.623 c3.164,3.164,4.906,7.369,4.906,11.842S494.393,201.559,491.23,204.722z"></path> </g> </g> </g></svg>`;

    // encoding from https://www.tutorialpedia.org/blog/drawing-an-svg-file-on-a-html5-canvas/#default-methods-to-draw-svg-on-html5-canvas
    const encodedSvg = encodeURIComponent(svg);
    const svgDataUrl = `data:image/svg+xml;charset=utf-8,${encodedSvg}`; 

    onMount(() => {
        const sc = Array.from(document.getElementsByClassName("fullscreen-container"))[0];
        sc.style.backgroundColor = hslToHex(h,s,v);

        const canvas = document.getElementById("svg-canvas");
        const ctx = canvas.getContext("2d");

        const WIDTH = canvas.width;
        const HEIGHT = canvas.height;

        function clear() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        }

        const FPS = 10;

        const NUM_ROWS = 3;
        const NUM_COLS = 3;
        const PLACEMENT_RANGE = 5;
        const WIDTH_SPACING = (WIDTH)/NUM_ROWS;
        const HEIGHT_SPACING = (HEIGHT)/NUM_COLS;

        const shapes = [];
        const JITTER_RANGE = 2;

        for (let row = 0; row < NUM_ROWS; row++) {
            for (let c = 0; c < NUM_COLS; c++) {
                const length = r(25, 50);
                const x = row*WIDTH_SPACING + Math.random() * PLACEMENT_RANGE;
                const y = c*HEIGHT_SPACING + Math.random() * PLACEMENT_RANGE;
                shapes.push({
                    "x": x,
                    "y": y,
                    "length": length,
                });
            }
        }

        function frame() {
            clear();

            shapes.forEach((shape) => {
                const xJitter = Math.random() * JITTER_RANGE - (JITTER_RANGE/2);
                const yJitter = Math.random() * JITTER_RANGE - (JITTER_RANGE/2);
                ctx.drawImage(img, shape.x, shape.y, shape.length + xJitter, shape.length + yJitter);
            });

            setTimeout(frame, 1000/FPS);
        }

        const img = new Image();

        img.onload = () => {
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
        max-height: 100%;
        overflow: hidden;
        box-sizing: border-box;
    }

    .page {
        display: grid;
        grid-template-rows: 2fr 8fr;
        justify-content: center;
        align-items: center;
    }

    h1 {
        text-align: center;
        z-index: 1;
    }

    p {
        text-align: center;
        z-index: 1;
    }

    #svg-canvas {
        position: fixed;
        top: 7.5%;
        left: 8.5%;
        width: 100%;
        height: 100%;
        min-height: 100%;
        overflow: visible;
        box-sizing: border-box;  
    }
</style>
<div class="fullscreen-container">
    <div class="page">
        <h1>
            Francis B Shiner
        </h1>

        <p>
            Hello! My name is Francis, and I am passionate about wool and singing. 
<br>
            You can find my Instagram <a href="https://www.instagram.com/knitbutch/">here</a> and my Ravelry <a href="https://www.ravelry.com/people/knitbutch">here</a>. 
<br>
            My friend Jeff designed this website, and you can find them <a href="https://jblake05.github.io">here</a>. 
        </p>         
    </div>
    <canvas id="svg-canvas">
    </canvas>
</div>

<!-- <Category data={data} cwd="misc"></Category> -->
