<script lang="ts">
  import AlbumCover from "../common/AlbumCover.svelte";
  import Heart from '../Heart/Heart.svelte'
  export let albums = [];
</script>

<style>
  ul {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(10rem, 1fr));
    grid-template-columns: repeat(auto-fill, minmax(8rem, 1fr));
    grid-auto-rows: 12.8rem;
    gap: var(--spacingMedium);
    list-style: none;
    max-width: 100%;
    padding: 0;
  }
  li {
    position: relative;
    display: flex;
  }
  .heart {
    position: absolute;
    bottom: calc(-1 * var(--spacingSmall));
    right: calc(-1 * var(--spacingSmall));
  }
</style>

<ul>
  {#each albums as album}
    <li>
      <AlbumCover {album} />
      {#if album.favorite}
        <div class="heart">
          <Heart />
        </div>
      {/if}
    </li>
  {/each}
</ul>
