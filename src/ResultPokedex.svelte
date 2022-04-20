<svelte:head>
	<link rel="icon" href={photo} />
</svelte:head>
<script>
import Abilities from "./Abilities.svelte";
export let photo = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png";
export let name = "bulbasaur";
export let type = "grass/poison";
export let weight = 360;
export let abilities = [
        "overgrow",
        "chlorophyll"
      ]
</script>
<style>
    div {
      display: flex;
      width: 100%;
      height: 100%;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      gap:10;
    }
    h2,p{
        text-transform: capitalize;
    } 
   .abilities{
        display: block;
        text-align: center;
        margin-bottom: 5px;
    }
</style>
<div>
    <img src={photo} alt={name} width="200"/>
    <h2>{name}</h2>
    <p>
        <b>Type: </b>
        {type}
        <b>Weight: </b>
        {weight}

     
    </p>
    <p>
        <b class="abilities">Abilities</b>
        {#each abilities as ability}
            <Abilities name={ability}/>
        {/each}
    </p>

</div>