<script>
    import { onMount } from 'svelte';
  
    // let data = {};

    export let data
    let resultados = null
    $: ({slug} = data)

    console.log(data)
  
    const fetchData = async () => {
        try {
        const response = await fetch(`https://api.api-ninjas.com/v1/exercises?difficulty=${data.slug}&offset=20`, {
            method: 'GET',
            headers: {
            'X-Api-Key': 'lrV4WBhJs5/OlAhQsYFs8g==o4Kuez08CU0BKCwH',
            'Content-Type': 'application/json',
            },
        });

        if (!response.ok) {
            throw new Error('Network response was not ok');
        }

        resultados = await response.json();
        console.log(resultados)
        } catch (error) {
        console.error('Error:', error);
        }
    };

    fetchData();

    
  </script>
  
  <main>
    <a href="/">Home</a>
    {#if resultados}
      {#each Object.entries(resultados) as [key, value] (key)}
        <p>{value.name}</p>
        <p>{value.type}</p>
        <p>{value.muscle}</p>
        <p>{value.equipment}</p>
        <p>{value.difficulty}</p>
        <p>{value.instructions}</p>
        <hr>
      {/each}
    {:else}
      <p>Loading...</p>
    {/if}
  </main>
