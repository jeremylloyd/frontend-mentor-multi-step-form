<script>
  export let inputId;
  export let plan;
  export let paymentFrequency;

  export let selected;
</script>

<label class='card' class:card--selected={selected == inputId} for={inputId}>
  <input type="radio" name='plan' id={inputId} bind:group={selected} value={inputId} required>
  <img class='card__icon' src={plan.icon} alt="icon-{inputId}">
  <div class='card__details'>
    <h3 class='card__title'>{plan.alias}</h3>
    <p class='card__desc'>${plan.rate[paymentFrequency]}/{paymentFrequency == 'month' ? 'mo' : 'yr'}</p>
    <h4 class='card__subtitle'>{paymentFrequency == 'year' ? '2 months free' : ''}</h4>
  </div>
</label>

<style>
  .card {
    flex-grow: 1;

    display: flex;
    align-items: flex-start;
    gap: 15px;
    border: solid 1px var(--grey);
    border-radius: 10px;
    padding: 15px;

    font-size: 0.9rem;
    cursor: pointer;
    user-select: none;
  }

  .card:active {
    border-color: var(--bluepurple);
  }

  .card__subtitle {
    font-size: 0.8rem;
    font-weight: 500;
    color: var(--bluemarine);
  }

  .card__title {
    font-size: 1rem;
    font-weight: 500;
    color: var(--bluemarine);
  }

  .card__desc {
    color: var(--grey);
  }

  input {
    opacity: 0;   /* Prefer this over display: none to show the form invalidation messages */
    position: absolute;
    z-index: -1;
  }

  .card--selected {
    background-color: hsla(243, 100%, 62%, 0.05);
    border: solid 1px var(--bluepurple);
  }

  @media screen and (min-width: 800px) {
    .card {
      flex-direction: column;
      height: 160px;
      max-width: 140px;
      justify-content: space-between;
    }
  }

  @media (hover: hover) {
    .card:hover {
      border-color: var(--bluepurple);
    }
  }
</style>