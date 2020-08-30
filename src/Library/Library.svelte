<script lang="ts">
  import { onMount } from "svelte";
  import Button from "../common/Button.svelte";
  import AlbumGrid from "../AlbumGrid/AlbumGrid.svelte";
  import { httpGet } from "../common/api";

  type Review = {
    author: string;
    stars: string;
    review: string;
  };

  type Album = {
    id: number;
    title: string;
    artist: string;
    cover: string;
    about: string;
    favorite: boolean;
    reviews: Review[] | [];
  };

  let albums: Album[] = [];

  onMount(async () => {
    const { data } = await httpGet("/?_sort=id$_order=desc");
    albums = data;
  });
</script>

<style>
  header {
    display: flex;
    justify-content: center;
    padding-top: 50px;
  }
  p {
    display: flex;
    justify-content: center;
  }
</style>

<header>
  <h1>Taylor Swift's Library</h1>
</header>
<p>View, favorite, and review Taylor Swift's albums!</p>
<AlbumGrid {albums} />
