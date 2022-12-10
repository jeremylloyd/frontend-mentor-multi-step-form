<script>
  export let pages = [];
  export let pageSelected = 1;

  import ButtonCircle from './ButtonCircle.svelte';
</script>

<div class="paginator">
  {#each pages as page}
    <ButtonCircle selected={pages.indexOf(page) + 1 == pageSelected}>
      {pages.indexOf(page) + 1}
    </ButtonCircle>
  {/each}
</div>

<style>
  .paginator {
    display: flex;
    gap: 15px;
    padding: 30px 0px;
  }
</style>
