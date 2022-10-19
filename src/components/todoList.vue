<script>
import Paginaton from './pagination.vue'
export default {
	data() {
		return {
			pageNumber: 1,
			todoQuantity: null,
			todoLimit: 10,
			pagesQuantity: null,
			pagination: [],
		}
	},
	props: {
		todos: Array,
	},
	components: { Paginaton },
}
</script>

<template>
	<ul class="todo-list">
		<div class="todo-title">Список дел:</div>
		<li
			:class="{
				'todo-item': true,
				'todo-item--success': todo.completed,
			}"
			v-for="todo in todos"
			:key="todo.id"
		>
			<div class="todo-content">
				<p :class="{ 'todo-line-through': todo.completed }">{{ todo.id }}: {{ todo.title }}</p>
			</div>
			<div class="todo-checked">
				<span>Todo completed: </span>
				<input type="checkbox" name="completed" :checked="todo.completed" />
			</div>
		</li>
	</ul>
</template>

<style scoped>
.todo-list {
	margin-top: 1em;
	list-style: none;
	background-color: rgb(78, 66, 66);
	padding: 1em 0.5em;
	border-radius: 1em;
}
.todo-item {
	display: flex;
	justify-content: space-between;
	align-items: center;
	padding: 0.75em;
	border-radius: 1em;
	background-color: rgb(170, 48, 17);
	gap: 1em;
}
.todo-item--success {
	background-color: rgb(43, 175, 43);
}
.todo-line-through {
	text-decoration: line-through;
}
.todo-title {
	font-size: 1.25em;
	margin-bottom: 1em;
	text-align: center;
}
.todo-item:not(:last-child) {
	margin-bottom: 0.5em;
}
.todo-checked {
	display: flex;
	align-items: center;
	justify-content: space-between;
	width: 250px;
	flex-shrink: 0;
}
</style>
