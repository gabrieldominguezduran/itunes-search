<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	interface SongType {
		trackName: string;
	}

	let song: SongType = {
		trackName: ''
	};

	onMount(async () => {
		let songId = $page.params.songId;

		const resultsFetched = await fetch(
			`https://itunes.apple.com/search?term=${songId}&entity=song`
		);
		const res = await resultsFetched.json();
		song = res.results[0];
		console.log(song);
	});
</script>

<section>
	<div>{$page.params.searched}</div>
	{song.trackName}
</section>
