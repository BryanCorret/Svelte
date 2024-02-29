<script>
    export let filter;
    export let departements;
    export let typesLieu;
    export let filterChanged;
  
    function applyFilter() {
      if (typeof filter.prixMax === 'string') {
        filter.prixMax = parseInt(filter.prixMax);
      }
      $: filter = { ...filter }; 
    }
  </script>
  
  <div class="row mt-5">
    <div class="col">
      <div class="input-group mb-3">
        <span class="input-group-text">Prix Max</span>
        <input type="number" class="form-control" bind:value={filter.prixMax} />
      </div>
    </div>
    <div class="col">
      <div class="input-group mb-3">    
        <label class="input-group-text" for="departementDropdown">Département</label>
        <select class="form-select" id="departementDropdown" bind:value={filter.departement}>
          <option value="">Choisir un département</option>
          {#each departements as departement}
            <option value={departement}>{departement}</option>
          {/each}
        </select>
      </div>
    </div>
    <div class="col">
      <div class="input-group mb-3">    
        <label class="input-group-text" for="typeLieuDropdown">Type de Lieu</label>
        <select class="form-select" id="typeLieuDropdown" bind:value={filter.typeLieu}>
          <option value="">Choisir un type de lieu</option>
          {#each typesLieu as typeLieu}
            <option value={typeLieu}>{typeLieu}</option>
          {/each}
        </select>
      </div>
    </div>
    <div class="col">
      {#if filterChanged || (filter.prixMax === undefined && filter.departement === "" && filter.typeLieu === "")}
        <button class="btn btn-primary" on:click={applyFilter}>Appliquer les filtres</button>
      {:else}
        <button class="btn btn-primary" on:click={applyFilter} disabled>Appliquer les filtres</button>
      {/if}
    </div>
  </div>
  