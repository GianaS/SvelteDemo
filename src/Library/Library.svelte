<script lang="ts">
  import { onMount } from "svelte";
  import Button from "../common/Button.svelte";
  import AlbumGrid from "../AlbumGrid/AlbumGrid.svelte";
  import { httpGet } from "../common/api";

  let albums = [];
  
  onMount(async () => {
    const { data } = await httpGet("/?_sort=id$_order=desc");
    albums = data;
  });
</script>

<header>
  <h1>Welcome, Swifties!</h1>
</header>

<p>You can view, favorite, and review Taylor Swift's albums!</p>

<Button>+ Add review</Button>
<AlbumGrid {albums} />
