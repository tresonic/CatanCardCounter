<script>
    import Cards from "svelte-material-icons/Cards.svelte";
    import Delete from "svelte-material-icons/Delete.svelte";
    import DiceMultiple from "svelte-material-icons/DiceMultiple.svelte";
    import Sprout from "svelte-material-icons/Sprout.svelte";
    import Modal, { getModal } from "./Modal.svelte";

    export let cards = 0;
    let diceThrow = 0;

    $: cardCount = cards.reduce((count, card) => count + card.count, 0);
    $: cardsToDiscard = cardCount > 7 ? Math.floor(cardCount / 2) : 0;
</script>

<div class="header">
    <span><Cards class="icon" /> {cardCount}</span>
    <span><Delete class="icon" />{cardsToDiscard}</span>
    <button on:click={() => {diceThrow=Math.floor(Math.random()*6+1) + Math.floor(Math.random()*6+1); getModal("dice").open()}}>
        <DiceMultiple class="icon" />
    </button>
    <Modal id="dice">
        <span>{diceThrow} gewürfelt!</span>
    </Modal>
    <button on:click={() => getModal("seed").open()}><Sprout class="icon" /></button>
</div>

<style>
    .header {
        width: 100%;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        column-gap: 2%;
        justify-content: center;
        align-items: center;
    }

    span {
        margin: 10px 5px;
        font-size: 25px;
    }

    button {
        height: 80%;
        padding: 5px 10px;
        font-size: 25px;
    }
</style>
