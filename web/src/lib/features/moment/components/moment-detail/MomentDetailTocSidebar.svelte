<script lang="ts">
	import type { TOCNode } from '$lib/shared/types/toc';
	import DetailTocNavList from '$lib/ui/detail/DetailTocNavList.svelte';
	import MomentDetailRelatedPosts from './MomentDetailRelatedPosts.svelte';

	interface Props {
		toc: TOCNode[];
		contentRoot: HTMLElement | null;
		activeAnchor: string | null;
		onAnchorChange: (anchor: string) => void;
	}

	let { toc, contentRoot, activeAnchor, onAnchorChange }: Props = $props();
</script>

<aside class="hidden lg:block pt-24 h-full relative slide-in-right">
	<div class="sticky top-24 space-y-10">
		{#if toc.length > 0}
			<div class="detail-sidebar-panel detail-sidebar-panel-moment space-y-5">
				<span
					class="block border-b border-slate-500/20 pb-2 font-mono text-[8px] font-bold tracking-[0.4em] text-pink-300/70 uppercase"
				>
					目录
				</span>
				<DetailTocNavList {toc} {contentRoot} {activeAnchor} {onAnchorChange} tone="cinnabar" />
			</div>
		{/if}

		<MomentDetailRelatedPosts />
	</div>
</aside>

<style lang="postcss">
	@reference "$routes/layout.css";

	.detail-sidebar-panel {
		border: 1px solid rgba(148, 163, 184, 0.12);
		padding: 1rem;
	}

	.detail-sidebar-panel-moment {
		background:
			linear-gradient(180deg, rgba(10, 16, 23, 0.88), rgba(7, 10, 15, 0.96)),
			radial-gradient(circle at top, rgba(244, 114, 182, 0.1), transparent 36%);
	}
</style>
