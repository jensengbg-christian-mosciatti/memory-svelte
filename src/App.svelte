<script>
  import { onMount } from "svelte";
  import Card from "./Card.svelte";
  import Overlay from "./Overlay.svelte";

  let cards = [];
  let pairs = 0;
  let numCards = 6;
  let pickedCards = [];
  let showOverlay = false;

  onMount(() => {
    disableview();
    createArray();
  });

  function createArray() {
    pairs = 0;
    cards = [];
    for (let i = 0; i <= numCards - 1; i++) {
      cards.push({
        id: i,
        flip: false,
        disableClick: false,
        dataCard: i + 1 > numCards / 2 ? i + 1 - numCards / 2 : i + 1
      });
    }
  }

  function cardData(event) {
    const obj = event.detail.card;

    if (pickedCards.length <= 2) {
      pickedCards.push(obj);
      cards[obj.id].flip = true;
      if (pickedCards.length === 2) {
        disableview(true);
        if (pickedCards[0].dataCard === pickedCards[1].dataCard) {
          pairs++;
          disableview();
          if (pairs === cards.length / 2) {
            setTimeout(() => {
              toggleOverlay();
            }, 300);
          }
        } else {
          const flipCards = [pickedCards[0].id, pickedCards[1].id];
          setTimeout(
            () => {
              cards[flipCards[0]].flip = false;
              setTimeout(() => {
                cards[flipCards[1]].flip = false;
                disableview();
              }, 200);
            },
            1500,
            flipCards
          );
        }
        pickedCards = [];
      }
    }
  }

  function toggleOverlay() {
    showOverlay = !showOverlay;
    if (!showOverlay) createArray();
  }

  function disableview(opt = false) {
    for (let card of cards) {
      card.disableClick = opt;
    }
  }
</script>

<style>

</style>

<div class="memory-cards">
  {#each cards as card}
    <Card bind:card {numCards} on:selectCard={cardData} />
  {/each}
  <Overlay bind:showOverlay on:overlay={toggleOverlay} />
</div>
