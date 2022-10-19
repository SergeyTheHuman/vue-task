<script>
import axios from 'axios'
export default {
	data() {
		return {
			todos: [],
			todoLimit: 10,
			todoQuantity: null,
			pageNumber: 1,
		}
	},
	methods: {
		getTodos(pageNumber = this.pageNumber, limit = this.todoLimit) {
			axios
				.get('https://jsonplaceholder.typicode.com/todos', {
					params: {
						_limit: limit,
						_page: pageNumber,
					},
				})
				.then((response) => {
					this.todoQuantity = response.headers['x-total-count']
					this.todos = response.data
				})
				.catch((e) => {
					console.log(error)
				})
		},
		setPage(newValue) {
			this.pageNumber = newValue
		},
	},
	watch: {
		pageNumber(newValue) {
			this.getTodos(newValue)
		},
	},
	mounted() {
		this.getTodos(this.pageNumber)
	},
	components: { Pagination, TodoList },
}
import Pagination from './components/pagination.vue'
import TodoList from './components/todoList.vue'
</script>

<template>
	<div class="wrapper" v-cloak>
		<Pagination v-if="todoQuantity" :limit="todoLimit" :todoQuantity="+todoQuantity" :setPage="setPage" :currentPage="pageNumber"> </Pagination>
		<TodoList v-if="todos.length" :todos="todos"></TodoList>
	</div>
</template>

<style>
* {
	padding: 0;
	margin: 0;
	box-sizing: border-box;
}
body {
	background-color: rgb(2, 2, 26);
	color: rgba(255, 255, 255, 0.85);
	font-size: 24px;
	font-family: Montserrat, san-serif;
}
[v-cloak] {
	display: none;
}
.wrapper {
	margin: 0 auto;
	max-width: 1200px;
	padding: 0.5em;
}
</style>
