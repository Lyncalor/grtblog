<script lang="ts">
	import { resolvePath } from '$lib/shared/utils/resolve-path';
	import { Calendar, FileText, ArrowRight } from 'lucide-svelte';
	import { momentDetailCtx } from '$lib/features/moment/context';
	import type { MomentRelatedPost } from '$lib/features/moment/types';
	import { buildPostPath } from '$lib/shared/utils/content-path';
	import { fly } from 'svelte/transition';

	const sameRelatedPosts = (
		a: MomentRelatedPost[] | null | undefined,
		b: MomentRelatedPost[] | null | undefined
	): boolean => {
		if (a === b) return true;
		if (!a?.length && !b?.length) return true;
		if (!a || !b || a.length !== b.length) return false;

		for (let i = 0; i < a.length; i += 1) {
			const left = a[i];
			const right = b[i];
			if (
				left.id !== right.id ||
				left.title !== right.title ||
				left.shortUrl !== right.shortUrl ||
				left.summary !== right.summary ||
				left.cover !== right.cover ||
				left.createdAt !== right.createdAt
			) {
				return false;
			}
		}

		return true;
	};

	const relatedPostsStore = momentDetailCtx.selectModelData((data) => data?.relatedPosts ?? [], {
		equals: sameRelatedPosts
	});

	function formatDate(dateStr: string) {
		const date = new Date(dateStr);
		return `${date.getMonth() + 1}月${date.getDate()}日`;
	}
</script>

<div class="related-panel related-panel-moment space-y-6">
	<div class="flex items-center justify-between border-b border-slate-500/20 pb-2">
		<div class="flex items-center gap-2">
			<FileText size={12} class="text-cinnabar-500" />
			<span class="font-mono text-[8px] font-bold tracking-[0.4em] text-ink-400 uppercase">
				同期文章
			</span>
		</div>
		<a
			href={resolvePath('/posts')}
			class="group text-[10px] text-slate-400 transition-colors hover:text-pink-200"
		>
			<ArrowRight size={10} class="transition-transform group-hover:translate-x-0.5" />
		</a>
	</div>

	{#if $relatedPostsStore.length === 0}
		<div
			class="rounded-default border border-dashed border-slate-500/20 bg-white/[0.02] p-3 text-[10px] text-slate-400"
		>
			暂无同期文章
		</div>
	{:else}
		<div class="space-y-4">
			{#each $relatedPostsStore as post, i (post.id)}
				<a
					href={resolvePath(buildPostPath(post.shortUrl))}
					class="group block space-y-1.5 rounded-default border border-slate-500/10 bg-white/[0.02] p-3 transition-all hover:border-pink-300/20 hover:bg-pink-400/[0.04] hover:shadow-sm"
					in:fly={{ x: 10, delay: i * 100 }}
				>
					<div class="flex items-center justify-between">
						<div class="flex items-center gap-1 text-[9px] font-medium text-ink-400">
							<Calendar size={10} strokeWidth={2} />
							{formatDate(post.createdAt)}
						</div>
					</div>
					<h4
						class="text-[11px] font-bold leading-snug text-slate-100 transition-colors group-hover:text-pink-200"
					>
						{post.title}
					</h4>
					<p class="line-clamp-2 text-[10px] leading-relaxed text-slate-400">
						{post.summary}
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
		padding: 1rem;
	}

	.related-panel-moment {
		background:
			linear-gradient(180deg, rgba(10, 16, 23, 0.88), rgba(7, 10, 15, 0.96)),
			radial-gradient(circle at top, rgba(244, 114, 182, 0.1), transparent 36%);
	}
</style>
