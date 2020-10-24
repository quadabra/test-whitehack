<!--accrodion item-->
<div class="card">
  <div class="card-header" id="headingOne">
    <h5 class="mb-0">
      <button class="btn btn-link" data-toggle="collapse" data-target={"#collapse" + $$props.id} aria-expanded="true" aria-controls="collapseOne">
        {$$props.name}
      </button>
    </h5>
  </div>
<!--expandable block-->
  <div id={"collapse" + $$props.id} class="collapse hide" aria-labelledby="headingOne" data-parent="#accordion">
    <div class="card-body">
      <div class="container-img">
        <img src="{$$props.image_url}" class="card-img-top responsive-img" alt="{$$props.name}">
      </div>
      <div>
        <h4>{$$props.tagline}</h4>
        <p>{$$props.description}</p>
        <p>abv: {$$props.abv}</p>
        <p>ibu: {$$props.ibu}</p>
        <p>target_fg: {$$props.target_fg}</p>
        <p>target_og: {$$props.target_og}</p>
        <p>ebc: {$$props.ebc}</p>
        <p>srm: {$$props.srm}</p>
        <p>ph: {$$props.ph}</p>
        <p>attenuation_level: {$$props.attenuation_level}</p>
        <p>tips: {$$props.brewers_tips}</p>
        <p>contributed_by {$$props.contributed_by}</p>
      </div>
    </div>
  </div>
</div>

<script>

</script>

<style>
  .container-img {
    margin-top: 2rem;
    height: 24rem;
  }

  .responsive-img {
    margin: 1em;
    display: block;
    width: auto;
    max-height: 100%;
  }

  .card-body {
    min-height: 12rem;
    display: flex;
    flex-direction: row;
  }

  .btn {
    margin: auto auto 0 0;
  }
</style>
