<script>
  import Icon from '@iconify/svelte';

  let taches = $state([]);
  let userTache = $state("");

  function deleteTache (idTache) {
    taches = taches.filter((tache) => tache.idTache !== idTache);
  }



  function addTache () {
    taches.push ({ 
      idTache: Date.now(), 
      texte: userTache,
      completee : false
    });
    console.table($state.snapshot(taches));
    userTache = "";
  }


</script>

<header>

  <h1>Planificateur de tâche</h1>

</header>

<main>

<div class="list">
  <div class="container-taches">
    {#each taches as tache }
      {#if !tache.completee}
    <div class="delete">
      <Icon icon="dashicons:arrow-right"/><input type="text" bind:value="{tache.texte}">
      <input type="checkbox" checked={tache.completee} onchange={() => tache.completee = !tache.completee}>
      <button class="deleteTache" onclick="{()=> deleteTache(tache.idTache)}"><Icon icon="dashicons:dismiss"/></button>
    </div>
      {/if}
    {/each}
<div class="container-taches-completee">
    {#each taches as tache }
      {#if tache.completee}
      <div class="tache-completee">
        <input type="text" bind:value="{tache.texte}"><input type="checkbox" checked={tache.completee} onchange={() => tache.completee = !tache.completee}>
      </div>
      {/if}
    {/each}
</div>
  </div>

    <div class="add">
      <input type="text" bind:value="{userTache}"><button class="addTache" onclick="{addTache}">Ajouter</button>
    </div>
</div>

</main>

<style>

  h1 {
    margin: 1rem 0;
    text-align: center;
  }

  .list {
    height: 720px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin: 0 2rem;
    padding: 1rem 0;
  }

  .container-taches {
    overflow: auto;
  }

  .add {
    margin-top: auto;
    display:flex;
    justify-content: space-between;
    align-items: center;
  }

  .delete {
    margin-bottom: 10px;
    display:flex;
    justify-content: space-between;
    align-items: center;
  }

  .tache-completee input {
    border: none;
    color: grey;
  }

  .container-taches-completee {
    margin-top: 10rem;
  }

</style>
