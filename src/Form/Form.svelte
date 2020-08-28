<script lang="ts">
  import { onMount } from "svelte";
  import { navigate } from "svelte-routing";
  import BackButtonRow from "../common/BackButtonRow.svelte";
  import AlbumCover from "../common/AlbumCover.svelte";
  import Button from "../common/Button.svelte";
  import Header from "../common/Header.svelte";
  import { httpPut, httpGet } from "../common/api.js";
  import TextInput from "./TextInput.svelte";
  import Review from "../Review/Review.svelte";

  export let id;

  let author = "";
  let stars = "";
  let review = "";

  $: fullReview = { author, stars, review };

  let album = {};
  let reviews = [];

  onMount(async () => {
    const { data } = await httpGet(`/${id}`);
    album = data;
    reviews = data.reviews;
  });

  const submitReview = async () => {
    const updatedAlbum = {
      ...album,
      reviews: [...reviews, fullReview],
    };
    const { ok } = await httpPut(`/${id}`, updatedAlbum);
    if (ok) {
      navigate(`/albums/${id}`);
    }
  };
</script>

<style>
  .pageWrapper {
  }
  form {
    display: grid;
    grid-auto-rows: auto;
    grid-template-columns: 1fr;
    gap: var(--spacingXLarge);
  }
  .fields {
    display: grid;
    grid-auto-rows: auto;
    gap: var(--spacingMedium);
  }
  .preview {
    display: grid;
    grid-template-columns: minmax(20vw, 10rem);
    grid-template-rows: minmax(32vw, 16rem);
  }
  @media (min-width: 48rem) {
    form {
      grid-template-columns: 60vw 20vw;
    }
  }
</style>

<div class="pageWrapper">
  <Header element="h1" size="large">Add Review for Album: {album.title}</Header>
  <form on:submit|preventDefault={submitReview}>
    <div class="fields" />
    <TextInput label="Name" bind:value={author} />
    <TextInput label="Stars" bind:value={stars} />
    <TextInput label="Review" bind:value={review} multiline />
    <div>
      <Button>Submit</Button>
    </div>
    <div>
      <Header>Preview</Header>
      <div class="preview" />
      <Review {fullReview} />
    </div>
  </form>
</div>
