<template>
	<v-app>
		<Todo/>
	</v-app>
</template>

<script setup>
	import Todo from '@/components/Todo.vue'
</script>

<style>
	html {
		scrollbar-width: thin;
		scrollbar-color: #FF2222 #00006d;
	}
	html::-webkit-scrollbar {
		width: 12px;
	}
	html::-webkit-scrollbar-thumb {
		background-color: #FF2222;
	}
	html::-webkit-scrollbar-track {
		background-color: #00006d;
	}
</style>