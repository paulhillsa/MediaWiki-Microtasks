<!-- Microtask 2 - Svelte -->
<!-- Source Form -->
<script>
	let input = '';
	let selected;
	let errorMessage = '';
	let inputNoDash;
	let sources = [
		{id: 0, type: 'Please select a source'},
		{id: 1 , type: 'Website (URL)'},
		{id: 2 , type: 'Book (ISBN)'},
		{id: 3 , type: 'Newspaper'},
		{id: 4 , type: 'Scientific Journal Article'},
		{id: 5 , type: 'Magazine Article'},
		{id: 6 , type: 'Other'}
	]

	function handleSubmit(e) {
		e.preventDefault();
		console.log(input);
		console.log(selected);

		// If no source is selected, show error message
		if (selected === 0) {
			errorMessage = 'Please select a source';
			return;
		}

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
		}
	}
</script>

<main>
	<!-- Error Message -->
	{#if errorMessage.length > 0}
			<p class="error-alert">{errorMessage}</p>
	{/if}

	<!-- Form -->
	<form on:submit|preventDefault={handleSubmit}> 
		<!-- User Input -->
		<input required type='text' name='input' bind:value={input} placeholder="Enter Source">
		<!-- Dropdown Source Type-->
		<select bind:value={selected}>
			{#each sources as source}
				<option value={source.id}>{source.type}</option>
			{/each}
		</select>
		<input type='submit' value='Submit'>
		<!-- Clear Button -->
		<button on:click={() => {
			input = '';
			selected = 0;
			errorMessage = '';
		}}>Clear</button>
	</form>
</main>

<style>

</style>