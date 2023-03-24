<template>
	<div class="flex flex-col h-scores p-6 lg:p-8 border-r-2 border-slate-200 bg-slate-50 xl:bg-white">
		<section class="flex flex-col w-matches gap-6">
			<h1 class="font-bold">{{ event }} Matches</h1>
			<h1 class="text-blue-700 cursor-pointer" @click="openURL(link)">View scorecard and details</h1>
			<div class="grid gap-4 grid-cols-1 justify-items-center py-3 border-x-2 border-t-2 rounded-t-xl text-lg" style="background-color: #FFC758; border-color: #FFC758;">
				<div class="font-bold">Previous Matches</div>
			</div>
		</section>
		<div class="flex flex-col border-2 border-slate-200 rounded-b-xl divide-y-2 divide-dashed w-matches h-matches overflow-y-scroll">
			<section v-for="i in cricket" :key="i">
				<div class="grid gap-4 grid-cols-4 justify-items-center text-slate-600 py-2">
					<div class="font-bold text-xs lg:text-base">{{ i.bat_team }}</div>
					<section class="flex gap-2 text-xs lg:text-base">
						<span>{{ i.t1_score }}</span>
					</section>
					<section class="flex gap-2 text-xs lg:text-base">
						<span>{{ i.t2_score }}</span>
					</section>
					<div class="font-bold text-xs lg:text-base">{{ i.bowl_team }}</div>
				</div>
			</section>
		</div>
	</div>
</template>

<script>
import axios from "axios"

export default {
	data() {
		return {
			cricket: []
		}
	},
	props: {
		event: String,
		link: String
	},
	created() {
		axios
			.get("https://raw.githubusercontent.com/Airo-MU/matches/master/cricket/cricket.json")
			.then((res) => {
				this.cricket = res.data
			})
	},
	methods: {
		openURL(url) {
			window.open(url);
		}
	},
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