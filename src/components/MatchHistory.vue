<template>
	<div class="flex flex-col h-scores p-6 lg:p-8 border-r-2 border-slate-200">
		<section class="flex flex-col w-matches gap-6">
			<h1 class="font-bold">{{ event }} Matches</h1>
			<div class="grid gap-4 grid-cols-1 justify-items-center py-3 border-x-2 border-t-2 rounded-t-xl text-lg" style="background-color: #FFC758; border-color: #FFC758;">
				<div class="font-bold">Previous Matches</div>
			</div>
		</section>
		<div class="flex flex-col border-2 border-slate-200 rounded-b-xl divide-y-2 divide-dashed w-matches h-matches overflow-y-scroll">
			<section v-for="i in 17" :key="i">
				<div class="grid gap-4 grid-cols-3 justify-items-center text-slate-600 py-2">
					<div class="font-bold text-xs lg:text-base">X{{ i }}</div>
					<section class="flex gap-2 text-xs lg:text-base">
						<span>{{ score }}</span>
					</section>
					<div class="font-bold text-xs lg:text-base">Y{{ i }}</div>
				</div>
			</section>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		event: String
	}
}
</script>


<style>
::-webkit-scrollbar {
	width: 0px;
	background: transparent;
}

.w-matches {
	width: 320px;
}

.h-matches {
	max-height: 506px;
}
</style>