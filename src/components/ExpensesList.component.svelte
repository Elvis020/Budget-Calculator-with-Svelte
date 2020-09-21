<script>
    import SectionTitle from '../shared/Title.component.svelte';
    import Expense from './Expense.component.svelte';
    
    export let inputExpenses = [];
</script>


<section>
    <SectionTitle title="expense list" />
    <ul>
        {#each inputExpenses as expense}
            <li> <Expense  {...expense} /> </li>
            {:else}
            <h2>You currently have no expenses... &#x1F607; </h2>
        {/each}
    </ul>
</section>


<style>
    h2{
        text-transform: capitalize;
    }
</style>
