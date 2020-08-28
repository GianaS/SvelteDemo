<script lang="ts">
  export let label;
  export let value;
  export let multiline: boolean = false;
</script>

<style>
  label {
    font-weight: var(--typeWeightBold);
    text-transform: uppercase;
  }
  span {
    padding: 0 0 var(--spacingSmall) var(--spacingLarge);
  }
  input,
  textarea {
    display: block;
    background: #f8ecde;
    border-radius: 25px;
    border: 2px solid var(--colorFg);
    padding: 0.75rem var(--spacingSmall) 0.75rem var(--spacingLarge);
    width: 100%;
  }
  textarea {
    height: 8rem;
  }
</style>

{#if multiline}
  <label>
    <span>{label}</span>
    <textarea type="text" bind:value />
  </label>
{:else}
  <label>
    <span>{label}</span>
    <input type="text" bind:value />
  </label>
{/if}
