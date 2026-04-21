<script lang="ts">
	import MarkdownView from '$lib/shared/markdown/MarkdownView.svelte';
	import { ChevronDown, Sparkles } from 'lucide-svelte';
	import { spring } from 'svelte/motion';

	interface Props {
		summary: string;
	}

	let { summary }: Props = $props();

	let isExpanded = $state(false);
	let contentHeight = $state(0);
	const summaryHeight = spring(60, { stiffness: 0.15, damping: 0.6 });

	$effect(() => {
		summaryHeight.set(isExpanded ? contentHeight : 60);
	});
</script>

<div
	class="detail-ai-summary mb-8 overflow-hidden rounded-default p-4 transition-all"
>
	<div class="mb-3 flex items-center justify-between gap-2.5">
		<div class="flex items-center gap-2">
			<div
				class="flex h-5 w-5 items-center justify-center rounded-md bg-sky-400/10 text-sky-200"
			>
				<Sparkles size={12} strokeWidth={2.5} />
			</div>
			<span
				class="font-mono text-[10px] font-bold tracking-widest text-sky-200 uppercase"
				>AI 摘要</span
			>
		</div>
		<button
			class="flex cursor-pointer items-center gap-1 select-none text-[10px] font-medium text-slate-300 transition-colors hover:text-sky-200"
			onclick={() => (isExpanded = !isExpanded)}
		>
			{isExpanded ? '收起' : '展开'}
			<ChevronDown
				size={12}
				class={`transition-transform duration-300 ${isExpanded ? 'rotate-180' : ''}`}
			/>
		</button>
	</div>
	<div
		class={`relative overflow-hidden will-change-[height] ${!isExpanded ? 'mask-gradient' : ''}`}
		style:height="{$summaryHeight}px"
	>
		<div
			bind:clientHeight={contentHeight}
			class="markdown-preview max-w-none font-sans text-xs leading-relaxed text-slate-300 [&>p]:mb-1.5 [&>p]:last:mb-0"
		>
			<MarkdownView content={summary} />
		</div>
	</div>
</div>

<style lang="postcss">
	@reference "$routes/layout.css";

	.detail-ai-summary {
		border: 1px solid rgba(148, 163, 184, 0.12);
		background:
			linear-gradient(180deg, rgba(10, 16, 23, 0.88), rgba(7, 10, 15, 0.96)),
			radial-gradient(circle at top right, rgba(56, 189, 248, 0.14), transparent 34%);
		box-shadow: 0 20px 40px -28px rgba(0, 0, 0, 0.8);
	}
</style>
