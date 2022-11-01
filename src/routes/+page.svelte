
<script>
    import '../app.css';
    import Results from '../components/results.svelte'
    
    let codes = [32,188,190,191,189];
    let [currentIndex,errors,speed] = [0,0,0];
    let [key,typed] = ['',''];
    let start,end,code,time,accuracy,active,state = 'false',color = 'yellow';
    let para = 
                'Lorem ipsum dolor sit amet consectetur, adipisicing elit. Voluptatibus inventore perspiciatis enim quibusdam cum ipsa labore ipsam quia reprehenderit reiciendis architecto facere, maiores consequuntur repellendus facilis itaque debitis, aliquam impedit?'

    function handleKeyDown (event) {
        if (event.which >= 65 && event.which <= 90 || codes.includes(event.which)) {
            key = event.key;
            code = event.which;
        }
        if (event.which == 32) {
            event.preventDefault();
        }
    }

    function showResults () {
        state = true;
    }

    function check (keyPressed,para) {
        if (currentIndex == 0) {
            start = new Date().getTime();
        }
        if (currentIndex == para.length-1) {
            end = new Date().getTime();
            setInterval (showResults,500)
            time = Math.round((end-start)/1000);
            accuracy =  Math.round(((para.length-errors)/para.length) * 100);
            speed = Math.round((para.length/5)/((end-start)/60000));
        }
        if (keyPressed == para[currentIndex]) {
            color = 'yellow';
            currentIndex ++;
        }
        else {
            color = 'red';
            errors ++;
        }
    }
    function reset () {
        [currentIndex,errors,time] = [0,0,0];
        [key,typed] = ['',''];
    }

    $: {
        if (key) {
            typed = para[currentIndex];
            check(key,para);
        }
    }

</script>

{#if state == true}
    <Results displayCover = 'block' displayBox = 'flex' accuracy = {accuracy} timeTaken = {time}
    errors = {errors} speed = {speed}/>
{/if}

<div class="bg-blue-200 h-auto box my-4 border-2 border-sky-500">
    <h1 class="text-sky-800 font-bold text-center">
        Typing Test
    </h1>
    <p class="text-sky-800 font-normal text-center">
        Start typing with the first letter of the paragraph. The results will appear after completion.
    </p>
</div>

<div class="mx-80 my-20 font-bold color1">
    {para}
</div>

<input class="font-bold" type="text" name="typed" value={typed} disabled>
<br><br>
<input style="color: {color};" class="font-bold" type="text" name="UserInput" value={key} disabled>

<h1 class="pt-10 font-bold text-center text-red-700">
    Errors : {errors}
</h1>

<div class="pt-10 font-bold text-center">
    <button on:click={reset} class="mx-2 px-2 py-1">
        Reset
    </button>
</div>

<style>
    :global(body) {
        background-color: #000957;
    }
    .color1 {
        color : #577BC1;
    }
    .box {
        width: 20rem;
        border-radius: 10px;
        margin-left: 32rem;
    }
    input {
        margin: 0 0 0 36rem;
        scale: 1.5;
    }
    button {
        border-radius: 10px;
        background-color: yellow;
        color: #000957;
    }
</style>

<svelte:window on:keydown={handleKeyDown}/>