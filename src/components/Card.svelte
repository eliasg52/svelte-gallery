<script lang="ts">
  export let image: any;
</script>

<div class="card" style="width: 18rem;">
  <img
    src={image.cover_photo.urls.thumb}
    class="card-img-top"
    alt={image.cover_photo.alt_description}
  />
  <div class="card-body">
    <a
      href={image.cover_photo.urls.full}
      target="_blank"
      class="btn btn-success">Visualizar imagen</a
    >
  </div>
</div>
