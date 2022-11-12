<script lang="ts">
	import { faker } from '@faker-js/faker';
	import { color } from "../lib/stores.js";
	export let name : string = faker.name.fullName();
	export let quote : string = faker.lorem.sentence();
</script>


<div class="flex flex-col p-8 border-2 rounded-md" style:border-color={$color}>
	<p>{name}</p>
	<p>{quote}</p>
</div>

