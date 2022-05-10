<script lang="ts">
	import { goto } from '$app/navigation';

	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	interface SongType {
		trackId: number;
		trackName: string;
	}

	let songsResults: SongType[] = [];

	onMount(async () => {
		let searched = $page.params.searched;

		const resultsFetched = await fetch(
			`https://itunes.apple.com/search?term=${searched}&entity=song`
		);
		const res = await resultsFetched.json();
		songsResults = res.results;
		console.log(songsResults);
	});
</script>

<section>
	<div>{$page.params.searched}</div>
	<div>
		{#each songsResults as song}
			<button on:click={() => goto(`${$page.params.searched}/${song.trackId}`)}>
				{song.trackName}
			</button>
		{/each}
	</div>
</section>
