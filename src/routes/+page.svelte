
<script>
    import '../app.css'

    let code,start,end;
    let status = false;
    let [currentIndex,time,speed,errors,accuracy] = [0,0,0,0,0];
    let codes = [32,188,190,191];
    let color = 'lightgreen';
    let [key,value,userInput] = ['',''];
    let para = 
                'Lorem ipsum dolor, sit amet consectetur adipisicing elit. Dolor dolorum adipisci veniam. Ipsa quisquam dolorum excepturi consequatur voluptatum vitae nostrum adipisci similique, accusamus totam. Accusamus beatae possimus fuga id officiis.'

    function handleKeyDown (event) {
        if (event.which >= 65 && event.which <= 90 || codes.includes(event.which)) {
            key = event.key;
            code = event.which;
            if (event.which == 32) {
                userInput = '';
            }
        }
    }

    function typing () {
        status = true
    }
    function notTyping () {
        status = false;
    }

    $: {
        if (key) {
            if (status) {
                if (currentIndex == 0) {
                    start = new Date().getTime();
                }
                if (currentIndex == para.length-1) {
                    end = new Date().getTime();
                    accuracy = Math.round((para.length - errors)/para.length) * 100;
                    time = Math.round((end-start)/1000);
                    speed = Math.round((para.length/5)/((end-start)/60000));

                }
                if (key == para[currentIndex]) {
                    color = 'lightgreen';
                    currentIndex ++; 
                    value += para[currentIndex-1];
                }
                else {
                    color = 'red';
                    errors ++;
                }
            }
        }
    }
</script>

<h1 class="title font-bold absolute">
    Typing test
</h1>

<div class="placeholder mx-80 my-20 font-bold" data-placeholder={para}>
    <textarea style="color: {color};" value={value}/> 
    <input on:focus={typing} on:focusout={notTyping} type="text" bind:value = {userInput}> 
    <a data-sveltekit-reload href='/' class="bg-black text-white p-1">Reset</a>
</div>


<div class="results bg-gray-100 text-gray font-800 text-center p-2">
    <h1>Accuracy : {accuracy} %</h1>
    <h1>Speed : {speed} <strong>WPM</strong></h1>
    <h1>Time Taken : {time} <strong>S</strong></h1>
    <h1>Erros : {errors}</h1>
</div>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Indie+Flower&family=Rampart+One&display=swap');

    textarea {
        resize: none;
        width: 100%;
        height: 80%;
        user-select: none;
    }
    input {
        border: 1px solid black;
        font-weight: 600;
        width: 50%;
        margin: 0vh 0vw 0vh 11vw;

    }
    a {
        border-radius: 10px;
    }
    .placeholder {
        position: relative;
        width: 50vw;
        height: 30vh;
    }

    .placeholder:focus {
        outline: none;
    }

    .placeholder::after {
        position: absolute;
        left: 0;
        top: 0;
        content: attr(data-placeholder);
        pointer-events: none;
        opacity: 0.6;
    }

    .results {
        margin: 20vh 0vw 0vh 42vw;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        width: 15vw;
        height: 25vh;
        scale: 1.5;
        border: 2px solid gray;
    }

    .title {
        scale: 1.5;
        font-family: 'Indie Flower', cursive;
        top: 1rem;
        left: 38rem;
    }
</style>
<svelte:window on:keydown={handleKeyDown}/>
