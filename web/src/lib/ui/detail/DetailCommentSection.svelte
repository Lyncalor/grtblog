<script lang="ts">
	import QueryRoot from '$lib/ui/common/QueryRoot.svelte';
	import Loading from '$lib/ui/common/Loading.svelte';

	interface Props {
		commentAreaId?: number | null;
		commentsCount?: number;
		fediverseObjectUrl?: string | null;
		containerClass?: string;
		fallbackText?: string;
		fallbackSize?: string;
		fallbackContainerClass?: string;
	}

	let {
		commentAreaId = null,
		commentsCount = 0,
		fediverseObjectUrl = null,
		containerClass = '',
		fallbackText = '评论区在赶来的路上...',
		fallbackSize = 'w-8 h-8',
		fallbackContainerClass = 'flex justify-center py-40'
	}: Props = $props();
</script>

{#if commentAreaId}
	<div class={`detail-comment-shell ${containerClass}`.trim()} data-comment-area>
		{#snippet commentFallback()}
			<div class={fallbackContainerClass}>
				<Loading size={fallbackSize} duration={1000} text={fallbackText} />
			</div>
		{/snippet}
		<QueryRoot
			loader={() => import('$lib/features/comment/components/CommentAreaClient.svelte')}
			loaderProps={{
				areaId: commentAreaId,
				commentsCount,
				fediverseObjectUrl
			}}
			fallback={commentFallback}
		/>
	</div>
{/if}

<style lang="postcss">
	@reference "$routes/layout.css";

	.detail-comment-shell {
		border-top-color: rgba(148, 163, 184, 0.16) !important;
		background: linear-gradient(180deg, rgba(255, 255, 255, 0.01), rgba(56, 189, 248, 0.03), rgba(255, 255, 255, 0.005));
	}
</style>
