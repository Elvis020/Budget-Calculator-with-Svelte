<script>
    import {getContext} from 'svelte';
   export let id;
   export let name="";
   export let amount=0;

   let displayAmount = false;

   const toggleAmount = () => {
    displayAmount = !displayAmount;
   }

   const removeExpense = getContext("remove")
   const setModifiedExpense = getContext("modifyExpense")
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2> {name} <button class="amount-btn" on:click={toggleAmount}><i class="fas fa-caret-down borderless"></i></button></h2>
        {#if displayAmount}
            <h4>Amount: ${amount} </h4>
        {/if}
    </div>
    <div class="expense-buttons">
        <button class="expense-btn edit-btn" on:click={() => setModifiedExpense(id) }>
            <i class="fas fa-pen"></i>
        </button>
        <button class="expense-btn delete-btn" on:click={() => removeExpense(id) }>
            <i class="fas fa-trash"></i>
        </button>
    </div>
</article>



<style>

    /* your styles go here */
</style>