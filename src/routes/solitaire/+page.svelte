<script lang='ts'>

	import data from './generate'





	import Card from './Card.svelte'
	import Pile_card from './Pile_card.svelte'
	import settings from '$lib/images/settings.svg';
	import arrow_right from '$lib/images/arrow_right.svg';
	import arrow_left from '$lib/images/arrow_left.svg';



	let draw_cycle = 0  

	let lower_deck_cells = [
		[...data.deck1],
		[...data.deck2],
		[...data.deck3], 
		[...data.deck4], 
		[...data.deck5], 
		[...data.deck6], 
		[...data.deck7], 
	]


	import { show_nav_bar } from '../store';
	import { show_footer } from '../store';
	import { createEventDispatcher } from "svelte"
	import { onMount } from 'svelte';
	onMount(async () => {

		console.log(data  )
		show_nav_bar.update(value => !value);

		//const dispatch = createEventDispatcher()
		//dispatch('started_game', {
		//    pressed: 'solitaire'
		//})
	});


	function draw(e){
		if(draw_cycle === 24){
			draw_cycle = 0
		}else{
			draw_cycle+=3;
			console.log(draw_cycle)
		}
	}
	const dropped_card = (e) => {
		
		let target = e.target


	}
</script>


<div id='main'>
	<div id='game_bar'>

	</div>
	<div id='game_board'>
		<div>
			<div id='settings_bar'>
				<div>
					<button class='options_buttons' ><img src={settings} alt="" /></button>
					<button class='options_buttons' >new game</button>
					<button class='options_buttons' >aa</button>
				</div>
				<div>
					<button class='options_buttons' >hint</button>
					<button class='options_buttons' ><img src={arrow_right} alt="" /></button>
					<button class='options_buttons' ><img src={arrow_left} alt="" /></button>
				</div>
			</div>
			<div id='upper_deck' >
				<!-- svelte-ignore a11y-click-events-have-key-events -->
				<div on:click={draw}>
					<div class='card'>
						<div class='flipped'>
						</div>
						<p id='remaining_cards' style='' > {24 - draw_cycle } </p>
						
					</div>
				</div>
				<div id='draw_pile' >
					{#if draw_cycle !== 0}
						{#each data.draw_pile.slice(draw_cycle-3, draw_cycle ) as card,i }
							<Pile_card index={i} card={card}   />
						{/each}
					{/if}
				</div>
				<div></div>
				<div></div>
				<div></div>
				<div></div>
				<div></div>
			</div>
			<div id='lower_deck' >
				{#each lower_deck_cells as deck, j }
					<div id={'lower_deck_'+(j)}  on:dragover|preventDefault on:drop|preventDefault={dropped_card} >
						{#each deck as card, i }
							{#if card.mode === 'flipped'}
								<div class='card' style={'top: '+i*50+'px'}>
									<div class='flipped'></div>
								</div>
							{:else}
								<Card index={i} card={card} drag={deck.length === i+1 ? true : false}  />
							{/if}
						{/each}
					</div>
				{/each}
			</div>
		</div>
	</div>
</div>

<style>
	#main{
		height: 100%;
	}
	#game_board{
		height: calc(100% - 50px );
		background-color: #219653ff;
		padding-top: 50px;
	}
	#game_board > :first-child{
		margin: auto;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		width: fit-content;
	}
	#settings_bar{
		width: 100%;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
	}
	#settings_bar > *{
		padding: 20px;
		padding-top: 5px;
		padding-bottom: 5px;
		display: flex;
		flex-direction: row;
	}
	.options_buttons{
		background-color: #3d4451;
		border: none;
		border-radius: 10px;
		font-size: 18px;
		padding: 10px;
		color: #a6adbaff;
		font-size: 16px;
		font-weight: 600;
		display: flex;
		align-items: center;
		justify-content: center;
		margin-right: 10px;
		cursor: pointer;
	}
	.options_buttons:last-of-type{
		margin-right: 0px; 
	}

	#upper_deck, #lower_deck{
		padding: 10px;
		display: flex;
		flex-direction: row;
		position: relative;
	}
	#upper_deck > *, #lower_deck > *{
		margin-right: 10px;
		margin-left: 10px;
		background-color: #276f46;
		aspect-ratio: 2/3;
		width: 100px;
		border-radius: 10px;
		position: relative;
	}
	#upper_deck > :nth-child(3){
		background-color: transparent;
	}

	.card{
		color:red;
		position: absolute;
		top: 0;
		left: 0;
		background-color: white;
		border-radius: 10px;
		width: 100%;
		height: 100%;
		padding: 5px;
		box-sizing: border-box;
		border: black 1px solid;
		cursor: pointer;
	}
	
	.flipped {
		border-radius: 10px;
		background-color: #eb5757ff;
		width: 100%;
		height: 100%;

	}
	.card_front{
		width: 100%;
		height: 100%;
	}
	.card_front > :first-child{
		padding-right: 2px;
		padding-left: 2px;
		height: 33%;
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;
	}
	.card_front > :first-child > :first-child {
		font-size: 38px;
		font-weight: 700;
		color: black;
	}
	.card_front > :first-child > :nth-child(2) {
		height: 90%;
	}
	.card_front > :nth-child(2){
		height: 67%;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.card_front > :nth-child(2) > :first-child{
		height: 100%;
	}


	#remaining_cards{
		
		font-size:25px;
		position:absolute;
		bottom: -20px; 
		right: 5px; 
		color:white;
		border-radius: 50%;
		padding: 5px;
		padding-left: 8px;
		padding-right: 8px;
		aspect-ratio: 1/1;
	}

</style>