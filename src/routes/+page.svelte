<script lang="ts">
    import { faker } from "@faker-js/faker";
    import { onMount } from "svelte";
    import { fly } from "svelte/transition";
    import { bgcolor, textcolor, names, sentences } from "../lib/stores.js"; 
    import Hero from './Hero.svelte';
    import Testimonials from './Testimonials.svelte';
	let components  = [
		{
			name: "Hero",
			component: Hero
		},
		{
			name: "Testimonials",
			component: Testimonials
		}
	];
	let layout = Hero;
    let backgroundColor : string = $bgcolor;
    let txtColor : string = $textcolor;
	let randomNames : string[];
	let randomSentences : string[];

    let sentenceInput1 : string;
    let sentenceInput2 : string;
    let sentenceInput3 : string;
    let isInputVisible : boolean = false;

	function randomize() {
		randomNames = [];
		randomSentences = [];
		for (let i = 0; i < 3; i++) {
			randomNames = [...randomNames, faker.name.fullName()];
			randomSentences = [...randomSentences, faker.hacker.phrase()];
		}
        sentenceInput1 = $sentences.at(0); 
        sentenceInput2 = $sentences.at(1);
        sentenceInput3 = $sentences.at(2);
    }

	$: names.set(randomNames);
	$: sentences.set(randomSentences);
    $: sentences.set([sentenceInput1, sentenceInput2, sentenceInput3]);
    $: bgcolor.set(backgroundColor);
    $: textcolor.set(txtColor);
    onMount(() => { 
        randomize(); 
    });

</script>

<div class="flex flex-col p-16 gap-8 w-full min-w-screen h-screen">
	<div class="flex flex-row mx-auto gap-8 h-1/12 align-center items-center">
        <select bind:value={layout} class="select select-bordered">
        {#each components as {name , component}}
            <option value={component}>{name}</option>
        {/each}
        </select>
        <div class="tooltip" data-tip="Background Color">
            <input 
                type="text" 
                placeholder={backgroundColor} 
                bind:value={backgroundColor}
                class="input input-md input-bordered w-full border-4"
                style:border-color={backgroundColor}
            />
        </div>
        <div class="tooltip" data-tip="Text Color">
            <input 
                type="text" 
                placeholder={txtColor} 
                bind:value={txtColor}
                class="input input-md input-bordered w-full border-4"
                style:border-color={txtColor}
            />
        </div>
        <button class="btn btn-primary" on:click={randomize}>Randomize</button>
        <input type="checkbox" bind:checked={isInputVisible} class="checkbox" />
    </div>	

    {#if isInputVisible}
        <div class="inline-block flex flex-row mx-auto gap-8 align-center items-center" transition:fly="{{y: -50, duration: 100}}" >
        <div class="tooltip" data-tip="Sentence 1">
        <input 
            type="text"
            placeholder={sentenceInput1}
            bind:value={sentenceInput1}
            class="input input-md input-bordered w-full"
            />
        </div>
        <div class="tooltip" data-tip="Sentence 2">
        <input 
            type="text"
            placeholder={sentenceInput2}
            bind:value={sentenceInput2}
            class="input input-md input-bordered w-full"
            />
        </div>
        <div class="tooltip" data-tip="Sentence 3">
        <input 
            type="text"
            placeholder={sentenceInput3}
            bind:value={sentenceInput3}
            class="input input-md input-bordered w-full"
            />
        </div>
    </div>
    {/if}

    <div class="transition-all duration-300 mockup-window border mx-auto h-5/6 w-full max-w-7xl">
		<div class="w-full h-full">
			<svelte:component this={layout} />
		</div>
	</div>
</div>
