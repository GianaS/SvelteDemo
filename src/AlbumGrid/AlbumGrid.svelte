<script lang="ts">
  import AlbumCover from "../common/AlbumCover.svelte";
  import Heart from "../Heart/Heart.svelte";
  export let albums = [];
</script>

<style>
  div {
    display: flex;
    justify-content: center;
  }
  ul {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 300px));
    grid-auto-rows: 12.8rem;
    grid-column-gap: 60px;
    grid-row-gap: 40px;
    list-style: none;
    max-width: 85%;
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
    border: 4px solid #E2DCDE;
    border-radius: 50%;
  }
</style>

<div>
  <ul>
    {#each albums as album}
      <li>
        <AlbumCover interactive {album} />
        {#if album.favorite}
          <div class="heart">
            <Heart />
          </div>
        {/if}
      </li>
    {/each}
  </ul>
</div>
