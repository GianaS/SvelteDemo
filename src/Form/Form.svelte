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
    display: flex;
    align-items: center;
    flex-direction: column;
    padding: 40px 0 40px 0;
  }
  form {
    width: 55%;
  }
  .fields {
    display: grid;
    grid-auto-rows: auto;
    gap: var(--spacingMedium);
    padding-top: 20px;
  }
  .preview {
    padding-top: 60px;
    width: 55%;
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
    <Button>Submit</Button>
  </form>
  <div class="preview">
    <Header>Preview</Header>
    <Review {fullReview} />
  </div>
</div>
