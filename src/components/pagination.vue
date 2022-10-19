<script>
export default {
	data() {
		return {
			pagination: [],
			totalPages: null,
		}
	},
	props: {
		limit: Number,
		todoQuantity: Number,
		currentPage: Number,
		setPage: Function,
	},
	methods: {
		getPagination() {
			this.pagination = []
			if (this.currentPage !== 1) this.pagination.push(1)
			if (this.currentPage >= 6) this.pagination.push(this.currentPage - 4)
			if (this.currentPage >= 4) this.pagination.push(this.currentPage - 2)
			this.pagination.push(this.currentPage)
			if (this.currentPage < this.totalPages - 2) this.pagination.push(this.currentPage + 2)
			if (this.currentPage < this.totalPages - 4) this.pagination.push(this.currentPage + 4)
			if (this.currentPage !== this.totalPages) this.pagination.push(this.totalPages)
		},
	},
	watch: {
		currentPage() {
			this.getPagination()
		},
	},
	mounted() {
		this.totalPages = Math.ceil(this.todoQuantity / this.limit)
		this.getPagination()
	},
}
</script>

<template>
	<div class="pagination">
		<button class="btn" :disabled="currentPage <= 1" @click="setPage(--currentPage)">Назад</button>
		<button
			class="btn"
			:class="{
				'btn--current': currentPage === pageNum,
			}"
			@click="setPage(pageNum)"
			v-for="pageNum in pagination"
			:key="pageNum"
		>
			{{ pageNum }}
		</button>
		<button class="btn" :disabled="currentPage >= totalPages" @click="setPage(++currentPage)">Вперед</button>
	</div>
</template>

<style scoped>
.pagination {
	display: flex;
	justify-content: center;
	align-items: center;
	gap: 0.5em;
}
.btn {
	background-color: transparent;
	border: 2px solid tomato;
	border-radius: 0.5em;
	font-size: 1.5rem;
	padding: 0.5em;
	color: rgba(255, 255, 255, 0.85);
}
.btn--current {
	background-color: transparent;
	user-select: none;
	border: 2px solid rgb(43, 175, 43);
}
.btn:disabled {
	opacity: 0.5;
}
</style>
