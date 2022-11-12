<script lang="ts">
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
</script>

<div class="flex flex-col p-16 gap-16 w-full min-w-screen h-full min-h-screen">
	<div class="flex flex-row mx-auto gap-8">
		{#each components as { name, component }}
			<label for={name} class="cursor-pointer text-lg text-center px-4">	
				<input id={name} type="radio" bind:group={layout} value={component} />
				{name}
			</label>
		{/each}
	</div>	
	<div class="flex flex-col border-8 border-gray-600 rounded-md ">
		<div class="flex flex-row px-8 justify-between top-0 inset-x-0 h-16 bg-gray-500">
			<div class="w-64 h-32 mt-4 bg-gray-400" />
			<div class="flex flex-row my-auto gap-4">				
				<div class="rounded-full w-4 h-4 bg-gray-600" />
				<div class="rounded-full w-4 h-4 bg-gray-600" />
				<div class="rounded-full w-4 h-4 bg-gray-600" />
			</div>
		</div>
		<div class="h-full aspect-video">
			<svelte:component this={layout} />
		</div>
	</div>	
</div>
