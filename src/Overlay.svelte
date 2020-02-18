<script>
  import { createEventDispatcher } from "svelte";
  export let showOverlay = false;
  const dispatch = createEventDispatcher();

  const close = () => {
    dispatch("overlay");
  };
</script>

<style>

</style>

<section class="overlay" class:show={showOverlay}>
  <a href="#" class="close" on:click={close}>X</a>
  <h1>You won!</h1>
</section>
