<script>

  let taches = $state([]);
  let userTache = $state("");

  function deleteTache (idTache) {
    taches = taches.filter((tache) => tache.idTache !== idTache);
  }



  function addTache () {
 taches.push({ idTache: Date.now(), texte: userTache });
    console.table($state.snapshot(taches));
    userTache = "";
  }


</script>

<header>

  <h1>Planificateur de tâche</h1>

</header>

<main>

<div class="list">
  {#each taches as tache }
  <div class="delete">
    <input type="text" value="{tache.texte}"><button class="deleteTache" onclick="{()=> deleteTache(tache.idTache)}">Supprimer</button>
  </div>
    {/each}

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
    margin: 0 1rem;
    padding: 1rem 0;
  }
</style>
