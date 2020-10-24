<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container">
    <a class="navbar-brand" href="https://github.com/quadabra/test-whitehack">Github repository</a>
    <form class="form-inline my-2 my-lg-0 ml-auto">
      <input
              bind:value={search}
              class="form-control mr-sm-2"
              type="search"
              placeholder="Search"
              aria-label="Search">
      <button
              on:click={(e) => {e.preventDefault(); onSearch(search)}}
              class="btn btn-outline-success my-2 my-sm-0"
              type="submit">
        Search
      </button>
    </form>
  </div>
</nav>

<script>
  import { createEventDispatcher } from 'svelte'

  const dispatch = createEventDispatcher()

  function onSearch(params) {
    dispatch('message', params)
    search = ''
  }

  let search = ''
</script>
