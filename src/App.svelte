<Navbar
        bind:search
        on:message={fetchBySearch}
/>
<div class="container">
  <p>Current search url - {searchUrl ? searchUrl : 'none'}</p>
  <nav aria-label="Page navigation example">
    <ul class="pagination">
      <li class="page-item"><a class="page-link" href="#">Previous</a></li>
      <li class="page-item"><a class="page-link" href="#">1</a></li>
      <li class="page-item"><a class="page-link" href="#">2</a></li>
      <li class="page-item"><a class="page-link" href="#">3</a></li>
      <li class="page-item"><a class="page-link" href="#">Next</a></li>
    </ul>
  </nav>
</div>
<main class="container">
  <ul class="container grid">
    {#await promise}
      <p>loading...</p>
    {:then items}
      {#if items}

        {#each items as item}
          <li>
            <ItemCard {...item}/>
          </li>
        {/each}
      {:else}
        <p>Nothing Found</p>
      {/if}
    {:catch error}
      <p>{error.message}</p>
    {/await}
  </ul>
</main>
<script>
  import { onMount } from 'svelte';
  import Navbar from './components/navbar.svelte'
  import ItemCard from './components/itemCard.svelte'

  const API_URL = 'https://api.punkapi.com/v2/beers'

  let search = ''
  let searchUrl = ''
  let pageNumber = 1
  const itemsPerPage = 24
  let promise = Promise.resolve([])

  async function fetchData(url) {
    const res = await fetch(url)
    if (res.ok) {
      return res.json()
    } else {
      throw new Error()
    }
  }

  function fetchByPage() {
    const URL = API_URL + '?page=' + pageNumber + '&per_page=' + itemsPerPage
    promise = fetchData(URL)
  }

  function fetchBySearch() {
    const URL = API_URL + '?beer_name=' + search
    promise = fetchData(URL)
    searchUrl = URL
  }

  onMount(() => {
    fetchByPage()
  })
</script>

<style>
  .grid {
    list-style: none;
    margin: 0;
    padding: 0;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: min-content;
    grid-gap: 1em;
  }
</style>
