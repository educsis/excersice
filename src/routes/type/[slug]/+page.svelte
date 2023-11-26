<script>
    import { onMount } from 'svelte';
  
    // let data = {};

    export let data
    let type = 'cardio';
    let resultados = null
    $: ({slug} = data)

    console.log(data)
  
    const fetchData = async () => {
        try {
        const response = await fetch(`https://api.api-ninjas.com/v1/exercises?type=${data.slug}&offset=20`, {
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

     
                
    <a href="/" class="btn btn-outline-primary">Home</a>
    <hr>
    {#if resultados}
      {#each Object.entries(resultados) as [key, value] (key)}
        <div class="row">
          <div class="col-md-12">
            <div class="card">
              <div class="card-body">
                <h5 class="card-title">{value.name}</h5>
                <h6 class="card-subtitle mb-2 text-muted">{value.type}</h6>
                  <p><strong>Muscle:</strong> {value.muscle}</p>
                  <p><strong>Difficulty:</strong> {value.difficulty}</p>
                  <p><strong>Instructions</strong> {value.instructions}</p>
              </div>
            </div>
          </div>
        </div>
        <br>
      {/each}
    {:else}
      <p>Loading...</p>
    {/if}
  </main>

  <!-- <main>
    <a href="/">Home</a>
    {#if resultados}
      {#each Object.entries(resultados) as [key, value] (key)}
        <p>{value.name}</p>
        <p>{value.type}</p>
        <p>{value.muscle}</p>
        <p>{value.equipment}</p>
        <p>{value.difficulty}</p>
        <p>{value.instructions.replace(/’/g, '&#x2019;')}</p>
        <hr>
      {/each}
    {:else}
      <p>Loading...</p>
    {/if}
  </main> -->
