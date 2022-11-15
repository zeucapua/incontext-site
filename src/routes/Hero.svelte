<script lang="ts">
	import { bgcolor, textcolor } from '../lib/stores.js';
	export let main : string = "Tiny Size. Huge Performance.";
</script>


<div class="h-full p-16" style:background-color={$bgcolor}>
	<div class="flex flex-col gap-8">
		<p class="text-8xl font-bold" style:color={$textcolor}>{main}</p>
	</div>
</div>
