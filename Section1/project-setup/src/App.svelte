<script>
	export let name;
	export let age;
	const thing = 'This is a test thing';

	function incrementAge() {
		age += 1;
	}
</script>

<style>
	h1 {
		color: purple;
	}
</style>

<h1>Hello {name}!, my age is {age}</h1>
<h2>{thing}</h2>
<button on:click="{incrementAge}">Change Age</button>
