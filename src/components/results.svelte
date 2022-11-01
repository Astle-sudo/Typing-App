<script>
    export let displayCover = 'none';
    export let displayBox = 'none';
    export let accuracy;
    export let timeTaken;
    export let errors;
    export let speed;
</script>

<div style="display: {displayCover};" class="cover bg-black"></div>
<div style="display: {displayBox};" class="box bg-blue-800 text-center m-0 p-0">
    <h1 class="color">Accuracy : {accuracy} %</h1>
    <h1 class="color">Time Taken : {timeTaken} <strong>Seconds</strong></h1>
    <h1 class="color">Errors : {errors}</h1>
    <h1 class="color">Speed : {speed} <strong>WPM</strong></h1>
</div>
<h1 class="bg-blue-800 text-center m-0 p-0 color ok px-3 py-2">
    <a data-sveltekit-reload href="/">Ok</a>
</h1>


<style>
    .cover {
        position: absolute;
        opacity: 0.8;
        z-index: 0;
        height: 95vh;
        width: 100vw;
        max-width: 100%;
        max-height: 100%;
    }
    .box {
        position: absolute;
        left: 42%;
        top: 30%;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        width: 12rem;
        height: 12rem;
        scale: 1.5;
        border-radius: 5px;
        z-index: 1;
    }
    .color { 
        color: yellow;
        font-weight: bold;
    }
    .ok {
        position: absolute;
        top: 70%;
        left: 48%;
        scale: 1.1;
        border-radius: 10px;
    }
    .ok:hover {
        cursor: pointer;
    }
</style>