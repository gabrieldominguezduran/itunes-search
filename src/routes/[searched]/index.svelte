<script lang="ts">
	import { goto } from '$app/navigation';

	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	interface SongType {
		trackId: number;
		trackName: string;
		artistName: string;
		artworkUrl100: string;
	}

	let songsResults: SongType[] = [];

	onMount(async () => {
		let searched = $page.params.searched;

		const resultsFetched = await fetch(
			`https://itunes.apple.com/search?term=${searched}&entity=song`
		);
		const res = await resultsFetched.json();
		songsResults = res.results;
	});
</script>

<section
	class="w-full min-h-screen bg-gradient-to-r from-yellow-600 via-pink-500 to-purple-500 px-10 md:px-20 lg:px-52 py-20"
>
	<div class="grid grid-cols-2 md:grid-cols-3 grod-flow row gap-3">
		{#each songsResults as song}
			<button
				on:click={() => goto(`${$page.params.searched}/${song.trackId}`)}
				class="p-3 flex bg-white rounded-md bg-opacity-20 border-2 border-white border-opacity-30"
			>
				<img src={song.artworkUrl100} alt="img" class="rounded-md mr-4 w-1/4" />
				<div class="flex flex-col items-start text-left">
					<div class="mb-2 h-6 overflow-hidden">{song.trackName}</div>
					<div class="text-xs font-bold">{song.artistName}</div>
				</div>
			</button>
		{/each}
	</div>
</section>
