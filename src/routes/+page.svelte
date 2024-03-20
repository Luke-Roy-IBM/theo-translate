<script>
	import translate from "translate";
	let inputtext = "";
	let outputtext = "";
	let inputlang = "de";
	let outputlang = "en";
	const languages = {
		"Deutsch": "de",
		"Englisch": "en",
		"Spanisch": "es",

	}
	translate.engine = "google";

	const text = translate("Hello world", "en");
	text.then((rsp) => {
		console.log(rsp);
	});
	// $: console.log(inputtext);

	let count = 0;

	function handleClick() {
		count += 1;
	}

	function translatetext() {
		const text = translate(inputtext, {from: inputlang, to: outputlang});
		text.then((rsp) => {
			// console.log(rsp);
			outputtext = rsp;
		});

	}
</script>


<h1><center>Translater</center></h1>

<button on:click={handleClick}>
	Clicked {count}
	{count === 1 ? "time" : "times"}
</button>
<center>
	<table style="width: 40%;">
		<tr>
			<th>
				<select bind:value={inputlang}>
				<option value="de">Deutsch</option>
				<option value="en">Englisch</option>
				<option value="es">Spanisch</option>
				</select>
			</th>

			<th>
				<select bind:value={outputlang}>
				{#each Object.entries(languages) as [title, lang]}
					<option value={lang}>{title}</option>
	
					
				{/each}
				</select>
			</th>
		</tr>

		<tr style="height: 100%;">
			<td
				><textarea rows="5" cols="50" bind:value={inputtext}
				></textarea></td
			>

			<td
				><textarea rows="5" cols="50" bind:value={outputtext}
				></textarea></td
			>
		</tr>
	</table>

	<button on:click={translatetext}>translate</button>
</center>

<style>
	table,
	th,
	td {
		border: 1px solid black;
		border-collapse: collapse;
	}
</style>
