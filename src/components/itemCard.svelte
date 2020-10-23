<div class="card" style="width: 100%">
  <div class="container-img">
  <img src="{$$props.image_url}" class="card-img-top responsive-img" alt="{name}">
  </div>
  <div class="card-body">
    <h5 class="card-title">{$$props.name}</h5>
    <p class="card-text">{$$props.tagline}</p>
    <a href="#" class="btn btn-primary">Details</a>
  </div>
</div>

<script>
  export let id

</script>

<style>
  .container-img {
    margin-top: 2rem;
    height: 24rem;
  }
  .responsive-img {
    margin: 1em auto;
    display: block;
    width: auto;
    max-height: 100%;
  }
  .card-body {
    min-height: 12rem;
    display: flex;
    flex-direction: column;
  }
  .btn {
    margin: auto auto 0 0;
  }
</style>
