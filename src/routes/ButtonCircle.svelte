<script>
  export let selected = false;
</script>

<button class="button button--circle" class:button--selected={selected}>
  <slot>

  </slot>
</button>

<style>
  .button {
    border: solid 1px white;
    color: white;
    background-color: transparent;
    width: 35px;
    height: 35px;
    border-radius: 50%;
    font-weight: 700;
    font-size: 14px;
  }

  .button--selected {
    color: var(--bluemarine);
    background: var(--magnolia);
    border: none;
  }
</style>