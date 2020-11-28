<script>
	import ContactCard from './ContactCard.svelte';
	export let name;
	export let age;

	$: uppercaseName = name.toUpperCase();

	$: console.log(name);

	$: if (name === 'Xavier') {
		age = 34;
	}

	function incrementAge() {
		age += 1;
	}

	function changeName() {
		name = 'Xavier';
	}

	function nameInput(e) {
		name = e.target.value;
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {uppercaseName}!, my age is {age}</h1>
<button on:click="{incrementAge}">Change Age</button>
<button on:click="{changeName}">Change Name</button>
<!-- <input type="text" value="{name}" on:input="{nameInput}"> -->
<input type="text" bind:value="{name}">

<ContactCard userName="{name}"></ContactCard>
