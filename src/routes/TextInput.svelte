<script>
  export let placeholder;
  export let name;
  export let label;
  export let type = 'text';

  let unfocused = false;
  let invalidLabel = "";
  let inputElem;

  const buildInvalidLabel = (validity) => {
    console.log("Checked validity")
    if (validity == null || validity.valid) {
      return ""
    } else if (validity.valueMissing) {
      return "This field is required"
    } else if (validity.typeMismatch) {
      return "Please input an email address"
    }
    return ""
  }
</script>

<div style="display: flex; flex-direction: column;" class:unfocused={unfocused}>
  <div class="labels">
    <label class="page__label" for="{name}">{label}</label>
    <div class="label-invalid">{invalidLabel}</div>
  </div>
  <input class="page__input-text" type="{type}" name="{name}" id="{name}" placeholder={placeholder} required bind:this={inputElem} on:blur={() => unfocused = true} on:input={() => invalidLabel = buildInvalidLabel(inputElem.validity)}>
</div>

<style>
  .label-invalid {
    font-size: 0.8rem;
    font-weight: 700;
    color: var(--red);
    opacity: 0;
  }

  .unfocused .label-invalid {
    opacity: 1;
  }

  .labels {
    display: flex;
    justify-content: space-between;
  }

  .page__label {
    font-size: 0.8rem;
  }

  .page__input-text {
    border: var(--greylight) solid 1px;
    padding: 5px 15px;
    font-size: 0.93rem;
    color: var(--bluemarine);
    font-weight: 500;
    border-radius: 5px;
    outline-width: 1px;
    transition: outline-color 0.2s ease-out;
  }
  
  .unfocused .page__input-text:invalid {
    outline: solid 1px red;
  }

  .page__input-text:focus {
    outline: solid 1px var(--bluepurple);
  }

  .page__input-text::placeholder {
    color: var(--grey);
  }
</style>
