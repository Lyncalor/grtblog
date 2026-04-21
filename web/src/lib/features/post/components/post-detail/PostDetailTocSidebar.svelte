<script lang="ts">
	import DetailTocNavList from '$lib/ui/detail/DetailTocNavList.svelte';
	import type { TOCNode } from '$lib/shared/types/toc';
	import PostDetailRelatedMoments from './PostDetailRelatedMoments.svelte';

	interface Props {
		toc: TOCNode[];
		contentRoot: HTMLElement | null;
		activeAnchor: string | null;
		onAnchorChange: (anchor: string) => void;
	}

	let { toc, contentRoot, activeAnchor, onAnchorChange }: Props = $props();
</script>

<aside class="hidden slide-in-right lg:block">
	<div class="sticky top-20 space-y-10">
		{#if toc.length > 0}
			<div class="detail-sidebar-panel space-y-5">
				<span
					class="block border-b border-slate-500/20 pb-2 font-mono text-[8px] font-bold tracking-[0.4em] text-sky-300/70 uppercase"
				>
					本页目录
				</span>
				<DetailTocNavList {toc} {contentRoot} {activeAnchor} {onAnchorChange} tone="jade" />
			</div>
		{/if}

		<PostDetailRelatedMoments />
	</div>
</aside>

<style lang="postcss">
	@reference "$routes/layout.css";

	.detail-sidebar-panel {
		border: 1px solid rgba(148, 163, 184, 0.12);
		background:
			linear-gradient(180deg, rgba(10, 16, 23, 0.88), rgba(7, 10, 15, 0.96)),
			radial-gradient(circle at top, rgba(56, 189, 248, 0.12), transparent 36%);
		padding: 1rem;
	}
</style>
