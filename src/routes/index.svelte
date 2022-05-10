<script lang="ts">
	import { goto } from '$app/navigation';
	let searched: string = '';

	const search = () => {
		goto(`${searched}`);
	};
</script>

<section>
	<div>
		<h1>Search an artist</h1>
		<input type="text" bind:value={searched} />
		<button on:click={search}>Search</button>
	</div>
</section>
