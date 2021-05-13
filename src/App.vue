<template>
	<div>
		<p>{{ msg }}</p>
		<span v-bind:title="msg">
			Hover your mouse over me for a few seconds to see my dynamically bound
			title!
		</span>
		<div>
			<button v-on:click="seen = !seen">
				<span v-if="seen">Hide</span><span v-if="!seen">Show</span>
			</button>
			<transition name="fade">
				<p v-if="seen">Now you see me</p>
			</transition>
		</div>
		<div>
			<ul v-for="(todo, index) in todos" :key="index">
				<li>
					ID: {{ todo.id }} Task: {{ todo.task }} Status: {{ todo.status }}
				</li>
			</ul>
			<form @submit.prevent="onSubmit">
				<input type="text" v-model="task" />
				<button>Add Task</button>
			</form>
		</div>
	</div>
</template>

<script>
export default {
	name: "App",
	data: function() {
		return {
			msg: "Naasdasdm",
			seen: true,
			todos: [
				{
					id: 1,
					task: "delectus aut autem",
					status: false,
				},
				{
					id: 2,
					task: "delectus aut autem",
					status: true,
				},
			],
			task: "",
		};
	},
	methods: {
		onSubmit() {
			this.todos.push({ id: 3, task: this.task, status: false });
		},
	},
};
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
	transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
	opacity: 0;
}
</style>
