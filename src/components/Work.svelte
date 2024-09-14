<script lang="ts">
	import Hideable from './Hideable.svelte';
	import type { IJob } from '../types';

	export let company: string = '';
	export let position: string = '';
	export let duration: string = '';
	export let period: string = '';
	export let jobs: IJob[] = [];
</script>

<Hideable>
	<div class="work-experience">
		<div class="mb-2 flex justify-start gap-4 font-bold print:mb-1">
			<p>{company}</p>
			<p>{duration}</p>
		</div>
		<div class="mb-2 flex justify-start gap-4 print:mb-1">
			<strong>{position}</strong>
			<span>{period}</span>
		</div>
		<ul class="list-disc pl-8 text-left print:pl-6">
			{#each jobs as job}
				<Hideable>
					<li>
						<strong>{job.label}</strong>
						<span>(Tech: {job.technologies.join(', ')})</span>
					</li>
					<ul class="list-disc pl-8 text-left print:pl-6">
						{#each job.details as detail}
							<Hideable>
								<li>{detail}</li>
							</Hideable>
						{/each}
					</ul>
				</Hideable>
			{/each}
		</ul>
	</div>
</Hideable>

<style lang="postcss">
	.work-experience {
		@apply my-4;
	}

	@media print {
		.work-experience {
			@apply my-1;
		}
	}
</style>
