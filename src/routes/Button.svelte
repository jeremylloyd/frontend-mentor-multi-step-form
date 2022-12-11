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
    transition: background-color 0.1s ease-out;
    font-weight: 500;
  }

  .button:active {
    background-color: var(--bluemarinelight);
  }

  .button--light {
    background: none;
    color: grey;
    min-width: unset;
  }
  
  .button--light:active {
    background: none;
    color: var(--bluemarine);
  }

  .button--primary {
    background-color: var(--bluepurple);
  }

  .button--primary:active {
    background-color: var(--bluepurplelight);
  }
</style>