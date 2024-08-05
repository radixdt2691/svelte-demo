<script>
    import { fade } from "svelte/transition";

    
    let txt = 'Welcome to ';
    let visible = true;
    let maintxt = 'SVELTE!!';
    let m = { x: 0, y: 0 };

    let bindvalue = 'Holaa Change me!!';

    let arrstu = [
        {name: 'Aman', marks: 75},
        {name: 'JG', marks: 80},
        {name: 'Gorab', marks: 60},
        {name: 'Ramesh', marks: 90},
        {name: 'Suresh', marks: 45},
        {name: 'Mahesh', marks: 50}
    ];

    let count = 0;

    $: if(count>=10){
        alert(`Count limit exceeded!!!`);
        count=9;
    }

</script>
<!-- {@debug arrstu} -->

<div>

    <label>
        <input type="checkbox" bind:checked={visible} />
        Toggle Heading Text
    </label>

    {#if visible}
        <h1 transition:fade class="d-flex align-center flex-wrap">{txt} <span>{maintxt}</span></h1>
    {/if}

    <div class="main-content d-flex align-stretch align-center flex-wrap">        
        <div>
            <h2>[#each ...]  Logic Blocks</h2>

            <ul>
                {#each arrstu as {name,marks},i}
                    <li>{i+1}: {name} - {marks}</li>
                {/each}
            </ul>
        </div>
    
        <div class="bind-wrapper">
            <h3>{bindvalue}</h3>
            <input type="text" bind:value={bindvalue}>
        </div>

        <div class="element-directive">
            <h3>on:click event</h3>

            <button on:click={()=>count+=1}>Click me to increse : {count}</button>        
        </div>

        <div class="dom-events" 	on:pointermove={(e) => {
            m = { x: e.clientX, y: e.clientY };
        }}>
            <h3>The Pointer is at {m.x} x {m.y}</h3>
        </div>
    </div>
</div>

<style>
    @font-face {
        font-family: 'Code';
        src: url('../fonts/SourceCodePro-Regular.woff2') format('woff2'), /* Super modern browsers */
             url('../fonts/SourceCodePro-Regular.woff') format('woff'), /* Modern browsers */
    }
    :global(body){
        font-family: 'Code',sans-serif;
        color: #c2bfbfee;
        height: 100vh;
        background-image: linear-gradient(to right bottom, #4a4a55, #6f4d79, #ae3f7c, #e62359, #ff3d00);
        background-repeat: no-repeat;
        background-size: cover;
    }
    
    .d-flex{
        display: flex;
        gap: 15px;
    }
    .flex-wrap{
        flex-wrap: wrap;
    }
    .align-center{
        justify-content: center;
        align-items: center;
    }
    .align-stretch{
        align-items: stretch;
    }
    .text-center{
        text-align: center;
    }
    span{
        font-size: 70px;
        background: #4A4A55;
        background: linear-gradient(to right, #000000 10%, #ff3c00 80%);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
    }
    .main-content{
        width: 100%;
        margin: 0 auto;
        padding: 10px;
        border: 2px dashed #3d3939;
        border-radius: 5px;
    }
    .main-content > div:not(:last-child){
        padding-right: 15px;
    }
    .main-content > div{
        position: relative;
    }
    button,input{
        border: 0;
        border-radius: 5px;
        padding: 10px 15px;
    }
    
    @media (max-width: 767px){
        .main-content{
            max-width: 400px;
            padding: 0;
        }
    }
    @media (min-width: 767px){
        .main-content{
            max-width: 650px;
        }
    }

    @media(min-width: 991px){
        .main-content{
            max-width: 890px;
        }
        .main-content > div:not(:last-child)::after{
        content: '';
        position: absolute;
        top: 0;
        right: 0;
        width: 2px;
        height: 214px;
        background: rgba(158, 153, 153, 0.521);
        }
    }

    @media (min-width: 1200px){
        .main-content{
            max-width: 1180px;
        }
    }
</style>