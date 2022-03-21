<script>
	import { wordsList } from './dict.js';
	var words = wordsList();
	words = words.map(name => name.toLowerCase());


	let length='';
	let greens='';
	let yellows='';
	let blacks='';

	var filtered;

	const handleChange = () => {
		filtered = words.filter(word => word.length == parseInt(length));
		filtered = filtered.filter(word => {
			for (var i = 0; i < greens.length; i++) {
				if ('a'<=greens.charAt(i) && greens.charAt(i)<='z')
				{
					if (word.charAt(i) != greens.charAt(i))
						return false;
				}
			}
			return true;

		});
		filtered = filtered.filter(word => {
			for (var i = 0; i < yellows.length; i++) {
				if (word.indexOf(yellows.charAt(i))==-1) {
						return false;
				}
			}
			return true;
		});
		filtered = filtered.filter(word => {
			for (var i = 0; i < blacks.length; i++) {
				if (word.indexOf(blacks.charAt(i))>-1) {
						return false;
				}
			}
			return true;
		});
	};


</script>

<main>
	<h1>welcome to worlde cheat!</h1>
	<h2>length</h2>
	<input bind:value={length} 
		placeholder="enter wordle length"
		on:change={handleChange}>
	<h2>greens</h2>
	<input bind:value={greens} placeholder="enter greens, _ for non determined" on:change={handleChange}>
	<h2>yellows</h2>
	<input bind:value={yellows} placeholder="enter yellows" on:change={handleChange}>
	<h2>blacks</h2>
	<input bind:value={blacks} placeholder="enter blacks" on:change={handleChange}>

	<p>{filtered}</p>
		
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
