<svelte:head>
	<title>Pokedex - Challenge - {name}</title>
</svelte:head>
<script>
	import ResultPokedex from './ResultPokedex.svelte';
	import {onMount} from "svelte";
	import InfiniteScroll from "./InfiniteScroll.svelte";
	let name = "bulbasaur";
	let attributesPokemon = {};
  	let count =0;
	let nextUrl =  '';
	let data = [];
	let newBatch = [];
	let src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png";
	async function fetchData() {
		const response = await fetch(`https://api.modyo.pokedex.hegga.tech/pokemon${nextUrl}`);
		const {data:{attributes}} = await response.json();
		newBatch = attributes.results;
		count = attributes.count;
		nextUrl = attributes.next;
	};
	
	onMount(()=> {
		fetchData();
	})

  $: data = [
		...data,
    ...newBatch
  ];
  async function handleClick(activeName) {
	name = activeName;
	const response = await fetch(`https://api.modyo.pokedex.hegga.tech/pokemon/${activeName}`);
	const {data:{attributes}} = await response.json();
	attributesPokemon = attributes;
  }
</script>

<style>
  main {
    display: flex;
    width: 100%;
    height: 100%;
    align-items: center;
    
    flex-direction: column;
  }
  div{
	width: 100%;
	padding: 0;
	margin: 0;
	-ms-box-orient: horizontal;
	display: flex;
	flex-wrap: wrap;
	align-items: center;
    justify-content: center;
	gap: 20px;
  }
  ul {
    box-shadow: 0px 1px 3px 0px rgba(0, 0, 0, 0.2),
      0px 1px 1px 0px rgba(0, 0, 0, 0.14), 0px 2px 1px -1px rgba(0, 0, 0, 0.12);
    display: flex;
    flex-direction: column;
    border-radius: 2px;
    width: 100%;
    max-width: 200px;
    max-height: 400px;
	background-color: white;
    overflow-x: scroll;
    list-style: none;
    padding: 0;
  }

  li {
    padding: 15px;
    box-sizing: border-box;
    transition: 0.2s all;
    font-size: 14px;
	cursor: pointer;
	text-transform: capitalize;
  }
  li.active {
    background-color: #eeeeee;
  }
  li:hover {
    background-color: #eeeeee;
  }
</style>

<main>

<img {src} alt="logo" />
  <h4>Infinite pokemon scroll - aiep challenge pokedex</h4>
 <div>
	<ul>
		{#each data as item}
		  <li on:click={handleClick(item.name)} class:active="{name === item.name}">{item.name}</li>
		{/each}
		<InfiniteScroll
		  hasMore={count}
		  threshold={100}
		  on:loadMore={() => { fetchData()}} />
	  </ul>
	<ResultPokedex  {...attributesPokemon} />
 </div> 
  

  <h5>
    Challenge pokedex 2022®
  </h5>
</main>
