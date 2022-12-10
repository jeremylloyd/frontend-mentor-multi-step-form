<script>
  export let placeholder;
  export let name;
  export let label;
</script>

<div style="display: flex; flex-direction: column;">
  <label class="page__label" for="{name}">{label}</label>
  <input class="page__input-text" type="text" name="{name}" id="{name}" placeholder={placeholder}>
</div>

<style>
  .page__label {
    font-size: 0.8rem;
  }

  .page__input-text {
    border: var(--greylight) solid 1px;
    padding: 5px 15px;
    font-size: 0.93rem;
    color: hsl(30, 4%, 19%);
    font-weight: 500;
  }
</style>
