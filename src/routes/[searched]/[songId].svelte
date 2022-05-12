<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	interface SongType {
		trackName: string;
		artworkUrl100: string;
		previewUrl: string;
	}

	let song: SongType = {
		trackName: '',
		artworkUrl100: '',
		previewUrl: ''
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

<section
	class="w-full min-h-screen bg-gradient-to-r from-yellow-600 via-pink-500 to-purple-500 px-10 md:px-20 lg:px-52 py-20"
>
	<div class="mt-12 flex flex-col items-center justify-center">
		<h1 class="text-3xl font-bold text-center mb-12">{song.trackName}</h1>
		<img src={song.artworkUrl100} alt="img" class="w-1/4 rounded-md mb-12" />
		<audio controls>
			<source src={song.previewUrl} type="audio/mpeg" />
		</audio>
	</div>
</section>
