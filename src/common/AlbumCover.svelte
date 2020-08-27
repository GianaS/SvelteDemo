<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import { links } from "svelte-routing";

  export let album = {};
  export let interactive = false;
</script>

<style>
  .book {
    --bg: #F1E4E8;
    --bgDark: #F1E4E8;
    --bgLight: #F1E4E8;

    background: #fff;
    border-radius: 4px;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.25);
    position: relative;
    transition: all 550ms;
    width: 100%;
    text-decoration: none;
  }

  .book--interactive {
    border: none;
    cursor: pointer;
  }
  .book--interactive:hover,
  .book--interactive:focus {
    filter: brightness(90%);
    outline: none;
  }

  .cover,
  .title {
    display: block;
  }
  .cover {
    background-image: linear-gradient(
      to right,
      var(--bgLight) 10%,
      var(--bg) 0%
    );
    background-size: cover;
    background-repeat: no-repeat;
    border-radius: 4px;
    color: #000;
    font-size: var(--typeSizeLarge);
    height: 300px;
    left: 0;
    overflow: hidden;
    text-align: left;
    text-transform: uppercase;
    text-shadow: 2px 2px 0 #fff;
    top: 0;
    transition: all 300ms;
    width: 300px;
  }

  .book--interactive:hover .cover,
  .book--interactive:focus .cover {
    box-shadow: 0.375rem 0.25rem 0.25rem rgba(0, 0, 0, 0.25);
    transform: translate(0.0625rem, -0.3125rem) skew(0, -5deg) scaleX(1.02);
  }
  .title {
    font-size: var(--typeSizeXLarge);
    font-weight: var(--typeWeightBold);
    line-height: var(--typeLineHeightTight);
    margin: 3rem 0 var(--spacingMedium) calc(10% + var(--spacingSmall));
  }
</style>

{#if interactive}
  <a
    href={`albums/${album.id}`}
    class="book book--interactive book--cover cover"
    use:links>
    <span
      class="cover"
      style={`background-image: url("/albumCovers/${album.cover}")`}>
      <span class="title">{album.title || ''}</span>
    </span>
  </a>
{:else}
  <div class="book book--cover cover">
    <span
      class="cover"
      style={`background-image: url("/albumCovers/${album.cover}")`}>
    </span>
  </div>
{/if}
