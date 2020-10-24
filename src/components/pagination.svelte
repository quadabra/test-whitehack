<nav aria-label="Page navigation example">
  <div class="container">
    <ul class="pagination justify-content-start">
      <li class="page-item" class:disabled="{current_page === 1}">
        <a
                class="page-link"
                on:click={() => changePage(current_page - 1)}
                href="javascript:void(0)"
                tabindex="-1">
          Previous
        </a>
      </li>
      {#each range(last_page, 1) as page}
        <li class="page-item">
          <a
                  class="page-link"
                  on:click={() => changePage(page)}
                  href="javascript:void(0)">
            {page}
          </a>
        </li>
      {/each}
      <li class="page-item" class:disabled="{current_page === last_page}">
        <a
                class="page-link"
                on:click={() => changePage(current_page + 1)}
                href="javascript:void(0)">
          Next
        </a>
      </li>
    </ul>
  </div>
</nav>

<script>
  export let current_page
  export let last_page

  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  function range(size, startAt = 0) {
    return [...Array(size).keys()].map(i => i + startAt);
  }

  function changePage(page) {
    if (page !== current_page) {
      dispatch('change', page)
      current_page = page
    }
  }
</script>
