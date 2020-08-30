<script lang="ts">
  import { links } from "svelte-routing";

  export let to: string;
</script>

<style>
  .button {
    background: var(--colorCta);
    border: none;
    border-radius: calc(
      (2 * (var(--spacingSmall) * 1.5) + var(--typeLineHeightTight)) / 2
    );
    color: var(--colorFgInverse);
    cursor: pointer;
    display: inline-block;
    font-size: var(--typeSizeSmall);
    font-weight: var(--typeWeightBold);
    line-height: var(--typeLineHeightTight);
    margin: 0;
    padding: calc(var(--spacingXSmall) * 1.5) var(--spacingMedium);
    text-overflow: ellipsis;
    transition: filter 150ms;
    white-space: nowrap;
    display: flex;
    align-items: center;
  }
  .button:hover,
  .button:focus {
    filter: brightness(115%);
    outline: none;
    text-decoration: none;
  }
</style>

{#if to}
  <a on:click class="button" href={to} use:links>
    <slot />
  </a>
{:else}
  <button on:click class="button">
    <slot />
  </button>
{/if}
