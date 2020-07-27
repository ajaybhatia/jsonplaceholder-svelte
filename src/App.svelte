<script>
  import { onMount } from "svelte";

  let photos;

  onMount(async () => {
    await fetch("https://jsonplaceholder.typicode.com/photos")
      .then(r => r.json())
      .then(data => (photos = data));
  });
</script>

<style>
  main {
    height: 100vh;
  }

  .container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  h1 {
    text-align: center;
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  .card {
    width: 200px;
    height: 200px;
    margin: 20px 10px;
  }

  .title {
    font-size: 0.9rem;
    text-overflow: ellipsis;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main>
  <h1>JSONPlaceholder</h1>

  <div class="container">
    {#if photos}
      {#each photos as photo, index}
        <div class="card">
          <img src={photo.thumbnailUrl} alt={`photo ${index + 1}`} />
          <p class="title">{photo.title}</p>
        </div>
      {/each}
    {/if}
  </div>
</main>
