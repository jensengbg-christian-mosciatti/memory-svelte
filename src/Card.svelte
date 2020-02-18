<script>
  import { createEventDispatcher } from "svelte";
  export let card = {};
  export let numCards = 0;

  const dispatch = createEventDispatcher();
  const selectCard = () => {
    flip();
    dispatch("selectCard", {
      card: card
    });
  };

  function flip() {
    card.flip = !card.flip;
  }
</script>

<style>

</style>

<article
  class:flip={card.flip}
  class:disable={card.disableClick}
  class="memory-card"
  style="order: {Math.floor(Math.random() * numCards) + 1}"
  on:click={selectCard}>
  <span class="front">{card.dataCard}</span>
  <span class="back">Memory</span>
</article>
