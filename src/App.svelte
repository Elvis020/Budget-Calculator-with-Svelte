<script>
	import Navbar from './components/Navbar.component.svelte';
	import Title from './shared/Title.component.svelte';
	import ExpenseForm from './components/ExpenseForm.component.svelte';
	import ExpensesList from './components/ExpensesList.component.svelte';
	import Totals from './components/Totals.component.svelte';
	import {setContext} from 'svelte';

	


	// data
	import expenseData from './Expenses';

	// Adding a reactive statement to check whether its editing or its adding an expense
	$: isEditing = setId ? true : false;

	// Adding reactive values in combination with the reduce function
	$: total =  expenses.reduce((acc, curr) => {
		return acc += curr.amount
	},0);


	// Variables
	let expenses = [...expenseData]
	// console.log(expenses);

	// Functions
	const removeExpense = (id) => {
		expenses = expenses.filter( (item) => item.id !== id )
	}

	// Function tpo add more Expenses to the expense list
	const addExpense =({name, amount})=>{
		let expense = {
			id: Math.random() * Date.now(),
			name,
			amount
		}
		expenses = [expense, ...expenses] 
	}

	// Setting editable variables
	let setId = null
	let setName = ''
	let setAmount = null


	// Toggling the Expense Form
	$: isFormOpen = false;


	// Function to control the toggling of the form
	const showForm =() => {
		// isFormOpen = !isFormOpen;
		isFormOpen = true;
	}
	// Function close the form
	const closeForm =() => {
		// isFormOpen = !isFormOpen;
		isFormOpen = false;
		setId = null;
		setName = '';
		setAmount = null;
	}


	// Function to modify/edit an expense
	const setModifiedExpense = (id) => {
		let modExpense = expenses.find(item => item.id === id)
		setId = modExpense.id;
		setName = modExpense.name;
		setAmount = modExpense.amount;
		showForm();
	}

	// Function to add a modified/edited an expense to the expense list
	const editExpense = ({name,amount}) => {
		expenses = expenses.map( item => {
			return item.id === setId? {...item, name, amount} : {...item}
		})
		setId = null;
		setName = '';
		setAmount = null;
	}





	// Setting up context to modify expense
	setContext('modifyExpense',setModifiedExpense)


	// Setting up context to remove expense
	setContext('remove',removeExpense)

	// Functio to clear all expenses
	const clearExpenses =() =>{
		expenses=[]
	}

</script>

<div>
	<Navbar {showForm} />
	<main class="content">
		{#if isFormOpen}
			<ExpenseForm {addExpense} name={setName} amount={setAmount} {isEditing} {editExpense} {closeForm} />
		{/if}
		<Totals title='total expenses' {total}/>
		<ExpensesList  inputExpenses={expenses} />
		<button type="button" class="btn btn-primary btn-block" on:click={clearExpenses} >Clear Expenses</button>
	</main>
	<!-- <Title title={"add expense"} /> -->
	<!-- <Title  /> -->




</div>

<style>
	
</style>