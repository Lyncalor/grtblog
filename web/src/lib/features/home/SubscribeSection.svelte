<script lang="ts">
	import { resolve } from '$app/paths';
	import { SlideIn } from '$lib/ui/animation';
	import { Mail, Rss } from 'lucide-svelte';
	import SubscribeModal from './SubscribeModal.svelte';

	let isModalOpen = $state(false);
</script>

<section class="mt-16 border-t border-slate-500/20 pt-16">
	<SlideIn direction="up">
		<div class="subscribe-terminal-shell flex flex-col md:flex-row items-center justify-between gap-8 px-4 py-8 md:px-8">
			<div class="flex flex-col gap-1 text-center md:text-left">
				<h2
					class="text-base font-serif font-medium text-white flex items-center justify-center md:justify-start gap-2 tracking-[0.12em] uppercase"
				>
					订阅更新
				</h2>
				<p class="text-[11px] text-slate-400 font-mono">
					欢迎通过邮件或 RSS 订阅，第一时间获取最新文章和手记等内容的更新通知。
				</p>
			</div>

			<div class="flex items-center gap-3">
				<button
					onclick={() => (isModalOpen = true)}
					class="px-5 py-2.5 text-xs font-medium bg-sky-500/85 text-slate-950 rounded-default hover:bg-sky-400 transition-all shadow-sm shadow-sky-500/20 flex items-center gap-2 group"
				>
					<Mail size={13} class="group-hover:rotate-12 transition-transform" />
					<span>邮件订阅</span>
				</button>

				<a
					href={resolve('/feed', {})}
					data-sveltekit-preload-data="off"
					class="px-5 py-2.5 text-xs font-medium bg-white/[0.03] border border-slate-400/20 text-slate-200 rounded-default hover:border-sky-300/40 hover:text-sky-200 transition-all flex items-center gap-2 group"
				>
					<Rss size={13} class="group-hover:text-amber-500 transition-colors" />
					<span>RSS 订阅</span>
				</a>
			</div>
		</div>
	</SlideIn>
</section>

<SubscribeModal bind:isOpen={isModalOpen} />

<style lang="postcss">
	@reference "$routes/layout.css";

	.subscribe-terminal-shell {
		border: 1px solid rgba(148, 163, 184, 0.14);
		background:
			linear-gradient(180deg, rgba(10, 16, 23, 0.88), rgba(7, 10, 15, 0.96)),
			radial-gradient(circle at top left, rgba(56, 189, 248, 0.12), transparent 30%);
		box-shadow: 0 22px 52px -28px rgba(0, 0, 0, 0.82);
		position: relative;
		overflow: hidden;
	}

	.subscribe-terminal-shell::before {
		content: '';
		position: absolute;
		inset: 0;
		pointer-events: none;
		background-image: linear-gradient(rgba(148, 163, 184, 0.05) 1px, transparent 1px);
		background-size: 100% 26px;
		opacity: 0.18;
	}
</style>
