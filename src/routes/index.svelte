<script lang="ts">
  import Loading from '../components/Loading.svelte';
  import Card from '../components/Card.svelte';

  let actualPage: number = 1;

  const getImages = async (page: number = 1) => {
    const response = await fetch(
      `https://api.unsplash.com/collections/?page=${page}&per_page=12&client_id=lTNeJB9Yq_F-NcuXX48x9TrVsLEEJ3M5SmuB0abQLPg`
    );
    const data = await response.json();

    return data;
  };

  let promise = getImages();

  const handleNextPage = () => {
    actualPage++;
    promise = getImages(actualPage);
  };

  const handlePreviousPage = () => {
    if (actualPage > 1) {
      actualPage--;
      promise = getImages(actualPage);
    } else {
      return;
    }
  };
</script>

<svelte:head>
  <title>Home - Page {actualPage}</title>
</svelte:head>

<div class="text-center">
  <h1>Galleria SK</h1>
  <hr />
  {#await promise}
    <Loading />
  {:then images}
    <div class="row">
      {#each images as image}
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
