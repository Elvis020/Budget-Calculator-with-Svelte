<script>
    import Title from "../shared/Title.component.svelte";
    // setting up two way binding
    export let name = '';
    export let amount = null;
    export let isEditing;
    export let  addExpense;
    export let editExpense;
    export let closeForm;
   

    $: isEmpty = !amount || !name
    const formSubmit = () => {
        if (isEditing){
            editExpense({name,amount})
            // console.log(editExpense);
        } else {
            addExpense({name,amount})
        }
        name = '';
        amount = null
    }
    
</script>


<section class="form">
    <Title title="add expenses"/>
    <form  class="expense-form" on:submit|preventDefault={formSubmit}>
        <div class="form-control">
            <label for="name">Name</label>
            <input type="text" bind:value={name} id="name">
        </div>
        <div class="form-control">
            <label for="amount">Amount</label>
            <input type="number" bind:value={amount} id="amount">
        </div>
        {#if isEmpty}
            <p class="form-empty">
                Please fill out all form fields
            </p>
        {/if}
        <button class:disabled={isEmpty} disabled={isEmpty} type="submit" class="btn btn-block">
            {#if isEditing}
                edit expense
                {:else}
                add expense
            {/if}
        </button>
        <button type="button" class="close-btn" on:click={closeForm}>
            <i class="fas fa-times"></i>
            close
        </button>
    </form>
</section>


<style>

</style>