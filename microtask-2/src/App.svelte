<!-- Microtask 2 - Svelte -->
<!-- Source Form -->
<!-- Language: svelte -->

<svelte:head>
	<!-- Font Imports -->
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Lato:wght@400;700&display=swap" rel="stylesheet">
</svelte:head>

<script>
	// Global Variables
	let input = '';
	let selected;
	let errorMessage = '';
	let inputNoDash;
	let sources = [
		{id: 1 , type: 'Website (URL)'},
		{id: 2 , type: 'Book (ISBN)'},
		/* Postponed
		{id: 3 , type: 'Newspaper'},
		{id: 4 , type: 'Scientific Journal Article'},
		{id: 5 , type: 'Magazine Article'},
		{id: 6 , type: 'Other'}
		*/
	]

	// Functions

	// Submit Function
	function handleSubmit(e) {
		e.preventDefault();
		console.log(input);
		console.log(selected);

		//Website
		if (selected === 1) {
			//Validate URL
			if (input === '') {
				errorMessage = 'Please enter a URL';
			}
			else if (input.includes('http://') || input.includes('https://')) {
				console.log('valid');
				errorMessage = 'Success!';
				//Send to server
			} else {
				console.log('invalid');
				errorMessage = 'Please enter a valid URL';
			}

		//Book
		} else if (selected === 2) {
			console.log('Book');
			// Remove dashes
			inputNoDash = input.replace(/-/g, '');
			//validation
			if (inputNoDash === '') {
				errorMessage = 'Please enter an ISBN';
				console.log('invalid');
			} else if (inputNoDash.length !== 10 && inputNoDash.length !== 13) {
				errorMessage = 'Please enter a valid ISBN';
				console.log('invalid');
			} else if (inputNoDash.length === 10) {
				console.log('valid');
				errorMessage = 'Success!';
			} else if (inputNoDash.length === 13) {
				console.log('valid');
				errorMessage = 'Success!';
			} else {
				errorMessage = 'Please enter a valid ISBN';
				console.log('invalid');
			}
		
		/* Postponed
		//Newspaper
		} else if (selected === 3) {
			console.log('Newspaper');
		//Scientific Journal Article
		} else if (selected === 4) {
			console.log('Scientific Journal Article');
		//Magazine Article
		} else if (selected === 5) {
			console.log('Magazine Article');
		//Other
		} else if (selected === 6) {
			console.log('Other');
		}
		else {
			errorMessage = 'Please select a source type';
		*/
		}
	}
</script>

<main>
	<div class='container'> 
	<!-- Form -->
	<form on:submit|preventDefault={handleSubmit}> 
		<!-- User Input -->
		<label class='required'for="quote">Source</label>
		<input class='text-input' required type='text' name='input' bind:value={input} placeholder="Enter Source">
		<!-- Dropdown Source Type-->
		<label for="source-type">Source Type</label>
		<select class='dropdown' bind:value={selected}>
			{#each sources as source}
				<option value={source.id}>{source.type}</option>
			{/each}
		</select>
		<!-- Error Message -->
		{#if errorMessage.length > 0}
			<p class="error-alert">{errorMessage}</p>
		{/if}
		<!-- Submit Button -->
		<button class='primary-progressive-btn' type="submit">Submit</button>
	</form>
	<!-- Clear Button -->
	<button class='destructive-btn' on:click={() => {
		input = '';
		selected = 1;
		errorMessage = '';
	}}>Clear</button>
	</div>
</main>

<style>
*{
	font-family: 'Lato', sans-serif;
	font-weight: 400;
}

label {
	font-weight: 700;
}

button {
	font-family: 'Lato', sans-serif;
	font-weight: 700;
	border-radius: 3px;
	border: none;
}

.container {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	width: 100%;
	height: 100%;
}

.primary-progressive-btn {
	color: white;
	background-color: #36c;
}

.primary-progressive-btn:hover {
	background-color: #3566F2;
	
}

.primary-progressive-btn:active {
	background-color: #2a4b8d;
}

.destructive-btn {
	color: white;
	background-color: #d33;
}

.destructive-btn:hover {
	background-color: #fb3329;
}

.destructive-btn:active {
	background-color: #b32424;
}

.text-input:hover {
	border-color: #72777d;
}

.text-input:focus, .text-input:active, .dropdown:focus, .dropdown:active {
	border-color: #36c;
}

.error-alert{
	font-weight: 400;
	color: #72777d;
}

.dropdown:hover {
	border-color: #72777d;
}

/* Remove baby blue background upon entering input */
input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus,
input:-webkit-autofill:active {
    transition: background-color 5000s ease-in-out 0s;
}

</style>