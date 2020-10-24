<!--item card-->
<div class="card" style="width: 100%">
  <div class="container-img">
    <img src="{$$props.image_url}" class="card-img-top responsive-img" alt="{$$props.name}">
  </div>
  <div class="card-body">
    <h5 class="card-title">{$$props.name}</h5>
    <p class="card-text">{$$props.tagline}</p>
    <button type="button" class="btn btn-outline-info" data-toggle="modal" data-target="{`#exampleModal` + $$props.id }">
      Show More
    </button>
  </div>
<!--modal info window. could be separate component but i failed-->
  <div class="modal fade" id="{`exampleModal` + $$props.id }" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="{`modalLabel` + $$props.id}">{$$props.name}</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <div class="modal-body__card">
            <div class="container-img">
              <img src="{$$props.image_url}" class="card-img-top responsive-img" alt="{$$props.name}">
            </div>
            <div class="card__description">
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
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        </div>
      </div>
    </div>
  </div>

</div>


<style>
  .container-img {
    margin-top: 2rem;
    height: 24rem;
  }

  .modal-body .container-img {
    height: 36rem;
    margin: 1rem;
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

  .modal-content {
    width: 1100px;
    transform: translateX(-27.5%);
  }

  .modal-body__card {
    display: flex;
    flex-direction: row;
  }

  .card__description {
    margin-left: 2rem;
  }

  .btn {
    margin: auto auto 0 0;
  }
</style>
