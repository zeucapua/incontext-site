<script lang="ts">
	import { bgcolor, textcolor, names, sentences } from "../lib/stores.js";

	let randomNames : string[] | undefined;
	let randomSentences: string[] | undefined;

	names.subscribe(list => { randomNames = list == undefined ? ["Jane Doe"] : list})
	sentences.subscribe(list => { randomSentences = list == undefined ? ["This is amazing!"] : list})

</script>


<div class="flex flex-row mx-8 my-auto p-8 gap-8 h-1/2">
	{#each (randomNames == undefined ? ["Jane Doe"] : randomNames) as name, i}
		<div class="relative flex flex-col justify-between rounded-lg w-1/3 h-full p-8 shadow-xl" style:background-color={$bgcolor}>
            <p class="absolute z-10 text-9xl bottom-0 text-black/10">🙶</p>
            <p class="text-2xl font-bold z-20" style:color={$textcolor}>
				{(randomSentences == undefined ? "This is awesome!" : randomSentences[i])}
			</p>
			<p class="text-md text-end" style:color={$textcolor}>- {name}</p>
		</div>
	{/each}
</div>

