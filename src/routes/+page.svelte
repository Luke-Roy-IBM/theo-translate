<script>
	import translate from "translate";
	import {
		Button,
		NativeSelect,
		Textarea,
		Container,
		Grid,
		Stack,
	} from "@svelteuidev/core";
	let inputtext = "";
	let outputtext = "";
	let inputlang = "de";
	let outputlang = "en";
	/* const languages = {
		Deutsch: "de",
		Englisch: "en",
		Spanisch: "es",
	}; */
	const languages = [
		{ label: "Deutsch", value: "de" },
		{ label: "Englisch", value: "en" },
		{ label: "Spanisch", value: "es" },
	];
	/*let person = {name: "Theo", age: 15, student: true}
	let persons = {student: [
		{name: ""}]}*/
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
		const text = translate(inputtext, { from: inputlang, to: outputlang });
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
	<table style="width: 80%;">
		<tr>
			<th>
				<NativeSelect
					data={languages}
					bind:value={inputlang}
					label="Select your output language:"
				/>

				<!-- <select bind:value={inputlang}>
					<option value="de">Deutsch</option>
					<option value="en">Englisch</option>
					<option value="es">Spanisch</option>
				</select> -->
			</th>

			<th>
				<NativeSelect
					data={languages}
					bind:value={outputlang}
					label="Select your output language:"
				/>

				<!--  
					{#each Object.entries(languages) as [title, lang]}
						<option value={lang}>{title}</option>
					{/each}
				</select>-->
			</th>
		</tr>

		<tr style="height: 100%;">
			<td>
				<Textarea placeholder="text" bind:value={inputtext} rows={5} />
				<!-- 
					<textarea rows="5" cols="50" bind:value={inputtext}></textarea>
			 -->
			</td>
			<td>
				<Textarea placeholder="text" bind:value={outputtext} rows={5} />
				<!-- <textarea rows="5" cols="50" bind:value={outputtext}></textarea> -->
			</td>
		</tr>
	</table>

	<!-- <button on:click={translatetext} >translate</button> -->
	<Button
		on:click={translatetext}
		variant="gradient"
		gradient={{ from: "blue", to: "violet", deg: 90 }}
		size="sm"
		uppercase
	>
		translate
	</Button>
</center>

<Container override={{ bc: "AliceBlue" }}>
	<Grid>
		<Grid.Col span={6}>
			<Stack override={{ height: 300 }}>
				<NativeSelect
					data={languages}
					bind:value={inputlang}
					label="Select your output language:"
				/>
				<Textarea placeholder="text" bind:value={inputtext} rows={5} radius="lg"/>
			</Stack>
		</Grid.Col>

		<Grid.Col span={6}>
			<Stack override={{ height: 300 }}>
				<NativeSelect
					data={languages}
					bind:value={outputlang}
					label="Select your output language:"
				/>
				<Textarea placeholder="text" bind:value={outputtext} rows={5} />
			</Stack>
		</Grid.Col>
	</Grid>
</Container>

<style>
	table,
	th,
	td {
		border: 1px solid black;
		border-collapse: collapse;
	}
</style>
