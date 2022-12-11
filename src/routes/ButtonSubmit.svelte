<script>
  export let variant = 'default';
  export let form;

  import Button from './Button.svelte';
</script>

<Button on:click type=submit form={form} variant={variant}>
  <slot></slot>
</Button>
