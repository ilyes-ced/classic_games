<script lang='ts'>
    import volume from '$lib/images/volume.svg';
    import moon from '$lib/images/moon.svg';
    import logo from '$lib/images/logo.svg';
    import { page } from '$app/stores';
    import { show_nav_bar } from './store';
	let show_nav: Boolean;

    $: current_page = $page.url.pathname

	show_nav_bar.subscribe(value => {
		show_nav = value;
	});


    let second_nav

    import { createEventDispatcher } from "svelte"
    const dispatch = createEventDispatcher()
    const test = (e) => {
        dispatch('button_changed', {
            pressed: e.target.innerText
        })
    }
    
</script>

<div class="navbar">
    <a href='/' id='logo'>
        <img src={logo}  alt="Welcome" />
    </a>
    <div>
        <button class='nav_buttons active_button' on:click={test} >play</button>
        <button class='nav_buttons' on:click={test} >idk yet</button>
    </div>
    <div id='right_icons'>
        <img src={volume} alt="Welcome" />
        <img src={moon} alt="Welcome" />
    </div>
</div>

<div id='second_nav_bar' bind:this={second_nav} style="translate: {current_page !== '/' ? '0px 0px': '0px -100px'}" >
    <a href='/solitaire'>SOLITAIRE</a>
    <a href='/2048'>2048</a>
    <a href='/mine_sweeper'>MINE SWEEPER</a>
    <a href='/breakout'>BREAKOUT</a>
    <a href='/tic_tac_toe'>TIC TAC TOE</a>
    <a href='/snake'>SNAKE</a>
    <a href='/'>all</a>
</div>

<style>
    .navbar > :first-child{
        width: 90px;
    }
    .navbar{
        padding-right: 20px;
        padding-left: 20px;
        padding-top: 10px;
        padding-bottom: 10px;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
    }
    .nav_buttons{
        padding-right: 15px;
        padding-left: 15px;
        padding-top: 5px;
        padding-bottom: 5px;
        border: 1px solid white;
        background-color: transparent;
        color: white;
        border-radius: 10px;
        font-size: 16px;
        font-weight: 600;
        cursor: pointer;
		transition: all 200ms cubic-bezier(.05,.43,.25,.95);
    }
    .nav_buttons:not(.active_button):hover{
        background-color: rgb(200, 200, 200);
        color: black;
    }
    .active_button:hover{
        background-color: aqua;
        color: rgb(200, 200, 200);
    }
    .active_button{
        color: aqua;
        border-color: aqua;
    }
    #right_icons{
        display: flex;
        align-items: center;
        justify-content: center;
    }
    #right_icons > *{
        padding: 10px;
        border-radius: 100%;
        cursor: pointer;
        border: 2px solid transparent;
		transition: all 200ms cubic-bezier(.05,.43,.25,.95);
    }
    #right_icons > *:hover{
        background-color: rgba(200,200,200,0.2);
        border-color: rgb(200, 200, 200);
    }



    #second_nav_bar{
        z-index: 100;
        background-color: #2a303c;

        width: 100%;
        padding-top: 10px;
        padding-bottom: 10px;
        height: 50px;
        position: absolute;
        top: 0;
        left: 0;
		transition: all 200ms cubic-bezier(.05,.43,.25,.95);


        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        
    }
    #second_nav_bar > *{
        text-decoration: none;
        color: #a6adbaff;
        padding: 20px;
        padding-top: 10px;
        padding-bottom: 10px;
        font-weight: 700;
        font-size: 16px;
        border-radius: 10px;
        cursor: pointer;
    }
    #second_nav_bar > *:hover{
        background-color: #3d4451;
    }


    #logo{
        z-index: 1000;
        height: 100%;
        display: flex;
        align-items: center;
        cursor: pointer;
    }
    #logo > img{
        width: 50px;
    }

</style>
