<script>
  export let variant = 'default';
  export let type = 'button';
  export let form = null;
</script>

<button class="button" class:button--light={variant == 'light'} class:button--primary={variant == 'primary'} on:click type={type} form={form}>
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
    min-width: 100px;
  }

  .button--light {
    background: none;
    color: grey;
    min-width: unset;
  }

  .button--primary {
    background-color: var(--bluepurple);
  }
</style>