<script lang="ts">
  import { onMount } from "svelte";

  import { httpGet, httpPut } from "../common/api";
  import BackButtonRow from "../common/BackButtonRow.svelte";
  import Header from "../common/Header.svelte";
  import Button from "../common/Button.svelte";
  import AlbumCover from "../common/AlbumCover.svelte";
  import Heart from "../Heart/Heart.svelte";
  import Review from "../Review/Review.svelte";
  import AlbumGrid from "../AlbumGrid/AlbumGrid.svelte";

  export let id;

  let album = {};
  let reviews = [];

  onMount(async () => {
    const { data } = await httpGet(`/${id}`);
    album = data;
    reviews = data.reviews ?? [];
  });

  const handleFavorite = async () => {
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
  .pageWrapper {
    padding: 0 40px;
    display: flex;
    align-items: center;
    flex-direction: column;
  }

  .detail {
    display: flex;
    justify-content: space-between;
    width: 55%;
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

  .header {
    padding-top: 40px;
    width: 55%;
  }

  .footer {
    width: 55%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 40px;
  }

  p {
    font-size: 20px;
    width: 450px;
  }

  h2 {
    margin-bottom: 0;
  }
</style>

<div class="pageWrapper">
  <div class="header">
    <BackButtonRow />
    <Header element="h1" size="large">Album Details</Header>
  </div>
  <div class="detail">
    <div class="cover">
      <AlbumCover {album} />
      <div class="favorite">
        <Button on:click={handleFavorite}>
          <img src={'/heart.png'} alt="taylor with heart hands" />
          {album.favorite ? 'Unfavorite' : 'Favorite'}
        </Button>
      </div>
    </div>
    <div>
      <Header>About</Header>
      <p>{album.about}</p>
    </div>
  </div>

  <div class="footer">
    <h2>Reviews</h2>
    <Button to={`/review/${album.id}`}>+ Add a review</Button>
  </div>

  {#each reviews as review}
    <Review {...review} />
  {/each}
</div>
