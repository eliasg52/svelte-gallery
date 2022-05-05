<script lang="ts">
  import Card from '../components/Card.svelte';
  import Loading from '../components/Loading.svelte';

  let ref: any;

  let actualPage: number = 1;
  let query: string = '';

  const getImages = async (page: number = 1, query: string = 'javascript') => {
    if (query.trim() === '') {
      return;
    }

    const response = await fetch(
      `https://api.unsplash.com/search/collections/?query=${query}&page=${page}&per_page=12&client_id=lTNeJB9Yq_F-NcuXX48x9TrVsLEEJ3M5SmuB0abQLPg`
    );
    const data = await response.json();

    return data;
  };

  let promise = getImages();

  const handleSubmit = () => {
    actualPage = 1;
    getImages(1, query);
    promise = getImages(actualPage, query);
  };

  const handleNextPage = () => {
    actualPage++;
    promise = getImages(actualPage, query);
  };

  const handlePreviousPage = () => {
    if (actualPage > 1) {
      actualPage--;
      promise = getImages(actualPage, query);
    } else {
      return;
    }
  };
</script>

<svelte:head>
  <title
    >Search {query.trim() === '' ? '' : `- ${query} Page ${actualPage}`}</title
  >
</svelte:head>

<form on:submit|preventDefault={handleSubmit} class="form-group row mb-3">
  <div class="col-12 col-md-8">
    <input
      bind:value={query}
      type="text"
      placeholder="Search a image"
      class="form-control"
      bind:this={ref}
      on:focus={() => ref.select()}
    />
  </div>
  <div class="col-12 col-md-4">
    <button class="btn btn-dark" type="submit">Search</button>
  </div>
</form>

<div class="text-center">
  {#await promise}
    <Loading />
  {:then images}
    <div class="row">
      {#each images.results as image}
        <div class="col-12 col-md-4">
          <Card {image} />
        </div>
      {/each}
    </div>
    {#if actualPage === 1}
      <button disabled class="btn btn-danger">Prev</button>
    {:else}
      <button on:click={handlePreviousPage} class="btn btn-danger">Prev</button>
    {/if}
    <button on:click={handleNextPage} class="btn btn-warning">Next</button>
  {/await}
</div>
