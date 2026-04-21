<script lang="ts">
	import { resolvePath } from '$lib/shared/utils/resolve-path';
	import { Calendar, NotebookPen, ArrowRight } from 'lucide-svelte';
	import { postDetailCtx } from '$lib/features/post/context';
	import { samePostRelatedMoments } from './selector-equals';
	import { buildMomentPath } from '$lib/shared/utils/content-path';
	import { fly } from 'svelte/transition';

	const relatedMomentsStore = postDetailCtx.selectModelData((data) => data?.relatedMoments ?? [], {
		equals: samePostRelatedMoments
	});

	function formatDate(dateStr: string) {
		const date = new Date(dateStr);
		return `${date.getMonth() + 1}月${date.getDate()}日`;
	}
</script>

<div class="related-panel space-y-6">
	<div class="flex items-center justify-between border-b border-slate-500/20 pb-2">
		<div class="flex items-center gap-2">
			<NotebookPen size={12} class="text-jade-500" />
			<span class="font-mono text-[8px] font-bold tracking-[0.4em] text-ink-300 uppercase">
				同期手记
			</span>
		</div>
		<a
			href={resolvePath('/moments')}
			class="group text-[10px] text-slate-400 transition-colors hover:text-sky-200"
		>
			<ArrowRight size={10} class="transition-transform group-hover:translate-x-0.5" />
		</a>
	</div>

	{#if $relatedMomentsStore.length === 0}
		<div
			class="rounded-default border border-dashed border-slate-500/20 bg-white/[0.02] p-3 text-[10px] text-slate-400"
		>
			暂无同期手记
		</div>
	{:else}
		<div class="space-y-4">
			{#each $relatedMomentsStore as moment, i (moment.id)}
				<a
					href={resolvePath(buildMomentPath(moment.shortUrl, moment.createdAt))}
					class="group block space-y-1.5 rounded-default border border-slate-500/10 bg-white/[0.02] p-3 transition-all hover:border-sky-300/20 hover:bg-sky-400/[0.04] hover:shadow-sm"
					in:fly={{ x: 10, delay: i * 100 }}
				>
					<div class="flex items-center justify-between">
						<div class="flex items-center gap-1 text-[9px] font-medium text-ink-400">
							<Calendar size={10} strokeWidth={2} />
							{formatDate(moment.createdAt)}
						</div>
					</div>
					<h4
						class="text-[11px] font-bold leading-snug text-slate-100 transition-colors group-hover:text-sky-200"
					>
						{moment.title}
					</h4>
					<p class="line-clamp-2 text-[10px] leading-relaxed text-slate-400">
						{moment.summary}
					</p>
				</a>
			{/each}
		</div>
	{/if}
</div>

<style lang="postcss">
	@reference "$routes/layout.css";

	.related-panel {
		border: 1px solid rgba(148, 163, 184, 0.12);
		background:
			linear-gradient(180deg, rgba(10, 16, 23, 0.88), rgba(7, 10, 15, 0.96)),
			radial-gradient(circle at top, rgba(56, 189, 248, 0.1), transparent 36%);
		padding: 1rem;
	}
</style>
