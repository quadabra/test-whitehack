<!--navbar with search input-->
<Navbar on:message={(e) => fetchBySearch({searchString: e.detail})}/>
<!--search url (for nothing)-->
<div class="container">
  <p>Current search url - {searchUrl ? searchUrl : 'none'}</p>
</div>
<!--pagination block-->
<Pagination
        bind:current_page={pageNumber}
        last_page={Math.ceil(itemsAmount/itemsPerPage)}
        on:change={(e) => changePage({page: e.detail})}>
</Pagination>

<main>
  <!--  layout switcher-->
  <div class="container">
    <div class="form-check form-check-inline">
      <input on:change={(e) => changeLayout(e)} class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1" value="list" checked>
      <label class="form-check-label" for="inlineRadio1">List</label>
    </div>
    <div class="form-check form-check-inline">
      <input on:change={(e) => changeLayout(e)} class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio2" value="grid">
      <label class="form-check-label" for="inlineRadio2">Grid</label>
    </div>
  </div>
<!--  beers list/grid-->
  <div class="container">
    <ul id="accordion" class="{layout === 'grid' ? 'grid' : 'list'}">
      {#await promise}
        <div class="d-flex align-items-center">
          <strong>Loading...</strong>
          <div class="spinner-border ml-auto" role="status" aria-hidden="true"></div>
        </div>
      {:then items}
        {#if items}
          {#each items as item}
            <li>
<!--              shows grid layout-->
              {#if layout === 'grid'}
                <ItemCard {...item}/>
<!--                shows list layout-->
              {:else if layout === 'list'}
                <ItemInfo {...item}/>
              {/if}
            </li>
          {/each}
        {:else}
          <p>Nothing Found</p>
        {/if}
      {:catch error}
        <p>{error.message}</p>
      {/await}
    </ul>
  </div>
</main>


<script>
  import { onMount } from 'svelte';
  import Navbar from './components/navbar.svelte'
  import ItemCard from './components/itemCard.svelte'
  import Pagination from './components/pagination.svelte'
  import ItemInfo from './components/itemInfo.svelte'


  const API_URL = 'https://api.punkapi.com/v2/beers' //base api url
  let layout = 'list' //init layout
  let searchUrl = '' // only to show URL with search done
  let pageNumber = 1 //init page
  const itemsAmount = 325 // experimental way found how many beers @api
  const itemsPerPage = 15 // <=25
  let promise = Promise.resolve([])

  function changePage(number) {
    fetchByPage(number.page, itemsPerPage)
  }
// function to change layout
  function changeLayout(e) {
    layout = e.target.value
  }
// fetch function
  async function fetchData(url) {
    const res = await fetch(url)
    if (res.ok) {
      return res.json()
    } else {
      throw new Error()
    }
  }
// function to fetch by pages
  function fetchByPage(number, items) {
    const URL = API_URL + '?page=' + number + '&per_page=' + items
    promise = fetchData(URL)
  }
// function to fetch by search (from navbar)
  function fetchBySearch(params) {
    const URL = API_URL + '?beer_name=' + params.searchString
    promise = fetchData(URL)
    searchUrl = URL
  }
// draws firs page
  onMount(() => {
    fetchByPage(pageNumber, itemsPerPage)
  })
</script>

<style>
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: min-content;
    grid-gap: 1em;
  }
</style>
