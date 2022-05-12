<script lang="ts">
	import { goto } from '$app/navigation';
	let searched: string = '';

	const search = () => {
		goto(`${searched}`);
	};
</script>

<section
	class="w-full min-h-screen bg-gradient-to-r from-yellow-600 via-pink-500 to-purple-500 px-10 md:px-20 lg:px-52 py-20"
>
	<div class="flex flex-col items-center justify-center">
		<div class="text-5xl text-center text-white font-semibold mb-12">Search an artist</div>
		<div
			class="w-full flex rounded-md bg-white bg-opacity-20 p-1 border border-white border-opacity-30"
		>
			<input class="w-4/5 bg-transparent text-white" type="text" bind:value={searched} />
			<button class="w-1/5 p-2 rounded-md bg-white font-medium" on:click={search}>Search</button>
		</div>
	</div>
</section>
