<script lang="ts">
	import { FadeIn } from '$lib/ui/animation';

	interface Props {
		title: string;
		subtitle?: string;
		description?: string;
		tag?: string;
		className?: string;
	}

	let { title, subtitle, description, tag, className = '' }: Props = $props();
</script>

<header class="page-header-shell relative mb-12 sm:mb-16 {className} px-4 py-8 sm:py-10">
	<FadeIn y={10} duration={800}>
		<div class="flex flex-col items-center text-center">
			<!-- Title Section -->
			<div class="relative flex flex-col items-center group">
				{#if tag}
					<span
						class="absolute -top-4 -right-8 [writing-mode:vertical-rl] text-[9px] font-mono font-bold text-sky-300/60 tracking-[0.3em] uppercase border-r border-sky-300/20 pr-1 h-10"
					>
						{tag}
					</span>
				{/if}

				<h1
					class="text-2xl md:text-4xl font-serif font-bold text-white tracking-[0.16em] uppercase"
				>
					{title}
				</h1>

				<!-- Subtle Underline Decor -->
				<div class="flex items-center gap-2 mt-3">
					<div class="w-1 h-1 rounded-full bg-sky-300/50"></div>
					<div class="w-12 h-px bg-sky-300/25"></div>
					<div class="w-1 h-1 rounded-full bg-sky-300/50"></div>
				</div>
			</div>

			{#if subtitle}
				<p
					class="mt-6 font-serif italic text-base text-slate-200 opacity-90 tracking-wide"
				>
					{subtitle}
				</p>
			{/if}

			{#if description}
				<div class="mt-4 flex items-start gap-3 max-w-lg">
					<span class="text-sky-300/35 font-serif text-lg leading-none">“</span>
					<p
						class="text-[13px] leading-relaxed text-slate-400 font-serif text-center italic"
					>
						{description}
					</p>
					<span class="text-sky-300/35 font-serif text-lg leading-none self-end">”</span>
				</div>
			{/if}
		</div>
	</FadeIn>
</header>

<style lang="postcss">
	@reference "$routes/layout.css";

	.page-header-shell {
		border: 1px solid rgba(148, 163, 184, 0.12);
		background:
			linear-gradient(180deg, rgba(10, 16, 23, 0.78), rgba(8, 12, 18, 0.9)),
			radial-gradient(circle at top, rgba(56, 189, 248, 0.1), transparent 36%);
		position: relative;
		overflow: hidden;
	}

	.page-header-shell::before {
		content: '';
		position: absolute;
		inset: 0;
		pointer-events: none;
		background-image:
			linear-gradient(rgba(148, 163, 184, 0.05) 1px, transparent 1px),
			linear-gradient(90deg, rgba(148, 163, 184, 0.05) 1px, transparent 1px);
		background-size: 28px 28px;
		opacity: 0.16;
	}
</style>
