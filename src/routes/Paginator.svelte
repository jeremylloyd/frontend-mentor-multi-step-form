<script>
  export let pages = [];
  export let pageSelected = 1;

  import ButtonCircle from './ButtonCircle.svelte';
</script>

<div class="paginator">
  {#each pages as page}
    <div class="paginator__item">
      <ButtonCircle selected={pages.indexOf(page) + 1 == pageSelected}>
        {pages.indexOf(page) + 1}
      </ButtonCircle>
      <div class="paginator__details">
        <div class="paginator__step">Step {pages.indexOf(page) + 1}</div>
        <div class="paginator__name">{page}</div>
      </div>
    </div>
    
  {/each}
</div>

<style>
  .paginator {
    display: flex;
    gap: 15px;
    padding: 30px 0px;
    z-index: 1;
  }

  .paginator__item {
    display: flex;
    align-items: center;
    gap: 20px;
  }
  
  .paginator__details {
    display: none;
    flex-direction: column;
    font-size: 0.9rem;
  }

  .paginator__step {
    color: var(--grey);
    text-transform: uppercase;
    font-size: 0.8rem;
  }

  .paginator__name {
    text-transform: uppercase;
    color: var(--alabaster);
    font-weight: 700;
    letter-spacing: 0.1rem;
  }

  @media screen and (min-width: 600px) {
    .paginator {
      flex-direction: column;
      margin-top: 10px;
    }

    .paginator__details {
      display: flex;
    }
  }
</style>
