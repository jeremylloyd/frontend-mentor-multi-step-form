<script>
  export let variant = 'default';
</script>

<button class="button" class:button--light={variant == 'light'} on:click>
  <slot></slot>
</button>

<style>
  .button {
    background-color: var(--bluemarine);
    color: var(--magnolia);
    padding: 10px 15px;
    border-radius: 5px;
    outline: none;
    border: none;
    font-size: 0.9rem;
    cursor: pointer;
  }

  .button--light {
    background: none;
    color: grey;
  }
</style>