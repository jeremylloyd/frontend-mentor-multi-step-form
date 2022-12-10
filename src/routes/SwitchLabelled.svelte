<script>
  import Switch from './Switch.svelte';

  export let checked;
</script>

<div class='flex-container'>
  <h3 class="toggle__label" class:toggle__label--checked={!checked}>Monthly</h3>
  <Switch bind:checked></Switch>
  <h3 class="toggle__label" class:toggle__label--checked={checked}>Yearly</h3>
</div>

<style>
  .flex-container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 25px;

    background-color: var(--alabaster);
    padding: 15px;
  }

  .toggle__label {
    font-size: 1rem;
    color: var(--grey);
    font-weight: 500;
    transition: color 0.2s ease-out;
  }

  .toggle__label--checked {
    color: var(--bluemarine);
  }
</style>