<script>
  export let addon = {};
  export let paymentFrequency;

  let id = `addon-${addon.id}`;
</script>

<label class='card' class:card--selected={addon.selected} for={id}>
  <input class='card__checkbox' type="checkbox" name="addon" id="{id}" bind:checked={addon.selected}>
  <div class='card__details'>
    <h3 class='card__title'>{addon.name}</h3>
    <p class="card__desc">{addon.description}</p>
  </div>
  <p class='card__price'>+${addon.rate[paymentFrequency]}/{paymentFrequency == 'month' ? 'mo' : 'yr'}</p>
</label>

<style>
  .card {
    display: flex;
    align-items: center;
    gap: 15px;
    border: solid 1px var(--grey);
    border-radius: 10px;
    padding: 15px;

    font-size: 0.85rem;
    cursor: pointer;
    user-select: none;
  }

  .card:active {
    border-color: var(--bluepurple);
  }

  .card__details {
    display: flex;
    flex-direction: column;
    margin-right: auto;
  }

  .card__title {
    font-weight: 700;
    font-size: inherit;
    color: var(--bluemarine);
  }

  .card__desc {
    color: var(--grey);
    font-size: 0.8rem;
  }

  .card__checkbox {
    accent-color: var(--bluepurple);
    width: 20px;
    height: 20px;
  }

  .card__price {
    font-size: 0.8rem;
    color: var(--bluepurple);
  }

  .card--selected {
    background-color: hsla(243, 100%, 62%, 0.05);
    border: solid 1px var(--bluepurple);
  }

  @media screen and (min-width: 800px) {
    .card {
      font-size: 1rem;
    }

    .card__desc {
      font-size: 0.9rem;
    }

    .card__price {
      font-size: inherit;
    }
  }
</style>