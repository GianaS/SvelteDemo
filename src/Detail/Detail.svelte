<script lang="ts">
  import { onMount } from "svelte";

  import { httpGet, httpPut } from "../common/api";
  import BackButtonRow from "../common/BackButtonRow.svelte";
  import Header from "../common/Header.svelte";
  import Button from "../common/Button.svelte";
  import AlbumCover from "../common/AlbumCover.svelte";

  export let id;

  let album = {};

  onMount(async () => {
    const { data } = await httpGet(`/${id}`);
    album = data;
  });

  const handleClick = async () => {
    const updatedAlbum = {
      ...album,
      favorite: !album.favorite,
    };
    const { ok } = await httpPut(`/${id}`, updatedAlbum);
    if (ok) {
      album = updatedAlbum;
    }
  };
</script>

<style>
  .detail {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(40vw, 20rem));
    gap: var(--spacingXLarge);
  }

  .cover {
    position: relative;
    margin-bottom: var(--spacingXLarge);
  }

  .favorite {
    width: 90%;
    margin-top: 20px;
  }

  img {
    width: 45px;
    height: 45px;
    margin-right: 10px;
  }
</style>

<BackButtonRow />
<Header element="h1" size="large">Album Details</Header>

<div class="detail">
  <div class="cover">
    <AlbumCover {album} />
    <div class="favorite">
      <Button on:click={handleClick}>
        <img src={'/heart.png'} alt='taylor with heart hands'/>
        {album.favorite ? 'Unfavorite' : 'Favorite'}
      </Button>
    </div>
  </div>
  <div>
    <Header>About</Header>
    <p>{album.about}</p>
  </div>
</div>
