<script>
	import { wordsList } from './dict.js';
	import { citiesList } from './citydict.js';
	import { nameList } from './firstname.js';

	var words = wordsList();
	var cities = citiesList();
	var names = nameList();

	cities = cities.map(city => city.toLowerCase().split(',')[0].replace(' ',''));
	names = names.map(name => name.toLowerCase().split(';')[0].replace(' ','').replace('+',''));
	words = words.map(name => name.toLowerCase());


	let length='';
	let greens='';
	let yellows='';
	let blacks='';

	var candi_words='';
	var candi_cities='';
	var candi_names='';

	const filtering = (words) => {
		var filtered = words.filter(word => word.length == parseInt(length));
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
		return filtered;	
	};

	const handleChange = () => {
		candi_words = filtering(words);
		candi_names = filtering(names);
		candi_cities = filtering(cities);
	};


</script>

<main>
	<h1>welcome to worlde cheat!</h1>
	<input type="button"
	value="search"	
		on:submit={handleChange}>
	<h2>length</h2>
	<input bind:value={length} 
		placeholder="length"
		on:change={handleChange}>
	<h2>greens, - for non determined</h2>
	<input bind:value={greens} placeholder="greens" on:change={handleChange}>
	<h2>yellows</h2>
	<input bind:value={yellows} placeholder="yellows" on:change={handleChange}>
	<h2>blacks</h2>
	<input bind:value={blacks} placeholder="blacks" on:change={handleChange}>
	<h2>words candidates</h2>
	<p>{candi_words}</p>
	<h2>cities candidates</h2>
	<p>{candi_cities}</p>
	<h2>names candidates</h2>
	<p>{candi_names}</p>

	<a href="https://github.com/evoka/wordlecheat">CODE</a>

		
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
		font-size: 2em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
