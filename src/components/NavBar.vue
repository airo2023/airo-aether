<template>
	<header class="sticky -top-0 flex px-6 py-4 border-b-2 border-slate-200 bg-white nav">
		<nav class="flex items-center justify-center lg:justify-between w-full">
			<ul class="hidden lg:flex gap-6">
				<li><a href="">Live Stream</a></li>
				<li><a href="">Gallery</a></li>
			</ul>
			<a href="https://www.instagram.com/aether_mu/" target="blank"><img src="../assets/logo.svg" class="w-8"></a>
		</nav>
	</header>

	<div class="fixed z-50 bottom-4 self-center flex items-center justify-center gap-4 lg:hidden bg-white p-4 rounded-full shadow-xl" @click="overflow = true">
		<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" v-if="overflow">
			<path d="M19 6.41L17.59 5L12 10.59L6.41 5L5 6.41L10.59 12L5 17.59L6.41 19L12 13.41L17.59 19L19 17.59L13.41 12L19 6.41Z" fill="black"/>
		</svg>
		<svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" v-else>
			<path d="M3 6H21V8H3V6ZM3 11H21V13H3V11ZM3 16H21V18H3V16Z" fill="black"/>
		</svg>
	</div>
	<div class="flex flex-col fixed z-50 inset-0 lg:hidden" v-if="overflow">
		<div class="fixed inset-0 bg-black/20 backdrop-blur-lg" @click="overflow = false"></div>
		<div class="flex flex-col fixed bottom-4 self-center text-base font-semibold">
			<button @click="overflow = false" class="absolute bottom-0 self-center flex items-center bg-white p-6 rounded-full shadow-md justify-center text-slate-500 hover:text-slate-600">
				<svg viewBox="0 0 10 10" class="w-2.5 h-2.5 overflow-visible" aria-hidden="true">
					<path d="M0 0L10 10M10 0L0 10" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"></path>
				</svg>
			</button>
			<ul class="flex flex-col mb-20 items-center gap-4 text-black">
				<li class="bg-white shadow-lg p-4 rounded-lg w-full text-center"><a class="hover:underline transition ease-in-out duration-300 cursor-pointer" href=""><a href="">Live Stream</a></a></li>
				<li class="bg-white shadow-lg p-4 rounded-lg w-full text-center"><a class="hover:underline transition ease-in-out duration-300 cursor-pointer" href=""><a href="">Gallery</a></a></li>
			</ul>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			overflow: false
		}
	}
}
</script>

<style>
.nav {
	width: calc(100vw - 62px);
	margin-left: 62px;
}
</style>