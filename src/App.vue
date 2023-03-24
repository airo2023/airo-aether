<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import MatchHistory from './components/MatchHistory.vue';
import NavBar from './components/NavBar.vue';
import CricketMatchHist from './components/CricketMatchHist.vue';
import ScoreCard from './components/ScoreCard.vue';
import CricketScore from './components/CricketScore.vue';
import TennisScore from './components/TennisScore.vue';
import TennisMatchHist from './components/TennisMatchHist.vue';
</script>

<template>
	<nav class="fixed z-50 flex flex-col gap-8 h-screen p-4 border-r-2 bg-white border-slate-200 overflow-hidden" :class="{'w-side': expand, 'w-16': !expand}">
		<button class="ml-1" @click="expand = !expand">
			<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
				<path d="M21 15.61L19.59 17L14.58 12L19.59 7L21 8.39L17.44 12L21 15.61ZM3 6H16V8H3V6ZM3 13V11H13V13H3ZM3 18V16H16V18H3Z" fill="black"/>
			</svg>
		</button>
		<ul class="ml-1 flex gap-6 flex-col text-slate-500">
			<li><span class="flex gap-6 items-center cursor-pointer" @click="reset(sportname[0])"><img src="./assets/cricket.svg"><h2>{{sportname[0]}}</h2></span></li>
			<li><span class="flex gap-6 items-center cursor-pointer" @click="reset(sportname[1])"><img src="./assets/basketball.svg"><h2>{{sportname[1]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[2])"><img src="./assets/badminton.svg"><h2>{{sportname[2]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[3])"><img src="./assets/football.svg"><h2>{{sportname[3]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[4])"><img src="./assets/volleyball.svg"><h2>{{sportname[4]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[5])"><img src="./assets/throwball.svg"><h2>{{sportname[5]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[6])"><img src="./assets/chess.svg"><h2>{{sportname[6]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[7])"><img src="./assets/tt.svg"><h2>{{sportname[7]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[8])"><img src="./assets/pool.svg"><h2>{{sportname[8]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[9])"><img src="./assets/snooker.svg"><h2>{{sportname[9]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[10])"><img src="./assets/kho.svg"><h2>{{sportname[10]}}</h2></span></li>
			<li><span class="gap-6 items-center cursor-pointer hidden" @click="reset(sportname[11])"><img src="./assets/tennis.svg"><h2>{{sportname[11]}}</h2></span></li>
		</ul>
	</nav>

	<div class="hidden lg:block fixed z-40 inset-0 w-screen h-screen bg-white/30 backdrop-blur-sm" v-if="expand" @click="expand = !expand"></div>

	<NavBar />
	<div class="flex flex-col lg:flex-row scores overflow-y-scroll">
		<CricketMatchHist class="hidden xl:block" :event="event" :link="link" v-if="cricket" />
		<TennisMatchHist class="hidden xl:block" :event="event" v-else-if="tennis || tt" />
		<div class="hidden xl:flex flex-col h-scores p-6 lg:p-8 border-r-2 border-slate-200" v-else>
			<section class="flex flex-col w-matches gap-6">
				<h1 class="font-bold">{{ event }} Matches</h1>
				<div class="grid gap-4 grid-cols-1 justify-items-center py-3 border-x-2 border-t-2 rounded-t-xl text-lg" style="background-color: #FFC758; border-color: #FFC758;">
					<div class="font-bold">Previous Matches</div>
				</div>
			</section>
			<div class="flex flex-col border-2 border-slate-200 rounded-b-xl divide-y-2 divide-dashed w-matches h-matches overflow-y-scroll">
				<section v-for="i in spSet" :key="i">
					<div class="grid gap-4 grid-cols-3 justify-items-center text-slate-600 py-2">
						<div class="font-bold">{{ i.team_1 }}</div>
						<section class="flex gap-2">
							<span>{{ i.running_score }}</span>
						</section>
						<div class="font-bold">{{ i.team_2 }}</div>
					</div>
				</section>
			</div>
		</div>

		<div class="flex flex-col gap-6 lg:gap-10 h-scores w-sc lg:w-full px-6 lg:px-12 py-6 bg-slate-50 border-r-2 border-slate-200 overflow-y-scroll">
			<div class="flex flex-col gap-3 lg:gap-6">
				<h1 class="font-bold text-slate-500">Recent</h1>
				<CricketScore :t1="spSet[0].bat_team" :t2="spSet[0].bowl_team" :score="spSet[0].running_score" :overs="spSet[0].overs" v-if="cricket" />
				<TennisScore t1="MU" t2="BITS" v-else-if="tennis || tt" />
				<ScoreCard :t1="spSet[0].team_1" :t2="spSet[0].team_2" :score="spSet[0].running_score" v-else />
			</div>
			<div class="flex flex-col gap-3 lg:gap-6">
				<h1 class="font-bold text-slate-500">Last Match</h1>
				<CricketScore :t1="spSet[1].bat_team" :t2="spSet[1].bowl_team" :score="spSet[1].running_score" :overs="spSet[1].overs" v-if="cricket" />
				<TennisScore t1="JNTU" t2="BITS" v-else-if="tennis || tt" />
				<ScoreCard :t1="spSet[0].team_1" :t2="spSet[0].team_2" :score="spSet[0].running_score" v-else />
			</div>
		</div>

		<div class="flex flex-col gap-6 h-scores p-6 lg:p-8 border-r-2 border-slate-200 bg-slate-50 xl:bg-white">
			<h1 class="font-bold">Standings</h1>
			<section>
				<section class="flex flex-col w-matches">
					<div class="grid gap-4 grid-cols-3 px-4 py-3 border-x-2 border-t-2 rounded-t-xl text-lg" style="background-color: #6BADDF; border-color: #6BADDF;">
						<div v-for="(k, ind) in set[0]" :key="k" class="font-bold">{{ ind }}</div>
					</div>
				</section>
				<div class="flex flex-col border-2 border-slate-200 rounded-b-xl divide-y-2 divide-dashed w-matches h-matches overflow-y-scroll">
					<section v-for="st in set" :key="st">
						<div class="grid gap-4 grid-cols-3 text-slate-600 px-4 py-2">
							<div v-for="i in st" :key="i">{{ i }}</div>
						</div>
					</section>
				</div>
			</section>
		</div>

		<CricketMatchHist class="xl:hidden block" :event="event" v-if="cricket" />
		<TennisMatchHist class="xl:hidden block" :event="event" v-else-if="tennis || tt" />
		<div class="xl:hidden flex flex-col h-scores p-6 lg:p-8 border-r-2 border-slate-200 bg-slate-50 xl:bg-white" v-else>
			<section class="flex flex-col w-matches gap-6">
				<h1 class="font-bold">{{ event }} Matches</h1>
				<div class="grid gap-4 grid-cols-1 justify-items-center py-3 border-x-2 border-t-2 rounded-t-xl text-lg" style="background-color: #FFC758; border-color: #FFC758;">
					<div class="font-bold">Previous Matches</div>
				</div>
			</section>
			<div class="flex flex-col border-2 border-slate-200 rounded-b-xl divide-y-2 divide-dashed w-matches h-matches overflow-y-scroll">
				<section v-for="i in spSet" :key="i">
					<div class="grid gap-4 grid-cols-3 justify-items-center text-slate-600 py-2">
						<div class="font-bold">{{ i.team_1 }}</div>
						<section class="flex gap-2">
							<span>{{ i.running_score }}</span>
						</section>
						<div class="font-bold">{{ i.team_2 }}</div>
					</div>
				</section>
			</div>
		</div>
	</div>
</template>

<script>
import axios from 'axios';
export default {
	data() {
		return {
			expand: false,
			event: "Cricket",
			link: "https://cricheroes.in/tournament/424723/AIRO-2K22",
			set: [],
			spSet: [],
			sportname: [
				"Cricket",
				"Basketball",
				"Badminton",
				"Football",
				"Volleyball",
				"Throwball",
				"Chess",
				"TT",
				"Pool",
				"Snooker",
				"KhoKho",
				"Tennis"
			],
			cricket: true,
			basketball: false,
			badminton: false,
			football: false,
			volleyball: false,
			throwball: false,
			chess: false,
			tt: false,
			pool: false,
			snooker: false,
			kho: false,
			tennis: false
		}
	},
	created() {
		axios
			.get("https://raw.githubusercontent.com/Airo-MU/matches/master/cricket/cricket.json")
			.then((res) => {
				this.spSet = res.data
			})
		axios
			.get("https://raw.githubusercontent.com/Airo-MU/matches/master/cricket/standings.json")
			.then((res) => {
				this.set = res.data
			})
	},
	methods: {
		callJSON(sp) {
			axios
			.get(`https://raw.githubusercontent.com/Airo-MU/matches/master/${sp}/${sp}.json`)
			.then((res) => {
				this.spSet = res.data
			})
			axios
			.get(`https://raw.githubusercontent.com/Airo-MU/matches/master/${sp}/standings.json`)
			.then((res) => {
				this.set = res.data
			})
		},
		reset(item) {
			this.expand = false
			this.cricket = false
			this.basketball = false
			this.badminton = false
			this.football = false
			this.volleyball = false
			this.throwball = false
			this.chess = false
			this.tt = false
			this.pool = false
			this.snooker = false
			this.kho = false
			this.tennis = false

			var inx = this.sportname.indexOf(item)
			switch (inx) {
				case 0:
					this.cricket = true;
					this.callJSON("cricket")
					this.event = this.sportname[0]
					break;
				case 1:
					this.basketball = true;
					this.callJSON("basketball")
					this.event = this.sportname[1]
					break;
				case 2:
					this.badminton = true;
					this.callJSON("badminton")
					this.event = this.sportname[2]
					break;
				case 3:
					this.football = true;
					this.callJSON("football")
					this.event = this.sportname[3]
					break;
				case 4:
					this.volleyball = true;
					this.callJSON("volleyball")
					this.event = this.sportname[4]
					break;
				case 5:
					this.throwball = true;
					this.callJSON("throwball")
					this.event = this.sportname[5]
					break;
				case 6:
					this.chess = true;
					this.callJSON("chess")
					this.event = this.sportname[6]
					break;
				case 7:
					this.tt = true;
					this.callJSON("tt")
					this.event = this.sportname[7]
					break;
				case 8:
					this.pool = true;
					this.callJSON("pool")
					this.event = this.sportname[8]
					break;
				case 9:
					this.snooker = true;
					this.callJSON("snooker")
					this.event = this.sportname[9]
					break;
				case 10:
					this.kho = true;
					this.callJSON("kho")
					this.event = this.sportname[10]
					break;
				case 11:
					this.tennis = true;
					this.callJSON("tennis")
					this.event = this.sportname[11]
					break;
				default:
					break;
			}
		}
	},
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

::-webkit-scrollbar {
	width: 0px;
	background: transparent;
}

#app {
	font-family: 'Montserrat', sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: black;
	display: flex;
	flex-direction: column;
}

.scores {
	max-width: calc(100vw - 62px);
	margin-left: 62px;
}

.h-scores {
	height: calc(100vh - 78.04px);
}

.w-side {
	width: 260px;
}

.standings {
	min-width: 360px;
}

.w-matches {
	width: 320px;
}

.h-matches {
	max-height: 506px;
}

@media (max-width: 1024px) {
	.scores {
		width: calc(100vw - 62px);
	}

	.h-scores {
		height: auto;
	}

	.w-sc {
		max-width: calc(100vw - 62px);
	}

	.w-matches {
		width: auto;
	}
}
</style>
