<script setup>
import { computed, ref } from 'vue';
import { projects } from '../lib/data.js';
import { Dot } from "lucide-vue-next"

// Pagination logic
const itemsPerPage = 4;
const currentPage = ref(1);
const totalPages = computed(() => Math.ceil(projects.length / itemsPerPage));
const paginatedProjects = computed(() =>
	projects.slice(
		(currentPage.value - 1) * itemsPerPage,
		currentPage.value * itemsPerPage
	)
);

</script>

<template>
	<div class="space-y-2 p-3 md:p-0">
		<h2 class="text-2xl font-semibold">Projects</h2>

		<!-- Education cards -->
		<div class="space-y-4 flex" v-for="project in paginatedProjects">
			<div class="card card-sm border border-gray-400 bg-base-100">
				<div class="card-body">
					<h2 class="card-title">{{project.title}}</h2>
					<p class="text-gray-300 font-semibold text-sm flex"><Dot />hola</p>
					<div class="badge badge-outline p-3 flex" v-for="tech in project.technologies">{{tech}}</div>
				</div>
			</div>
		</div>

		<!-- Pagination controls -->
		<div v-if="totalPages > 1" class="flex justify-center space-x-2 mt-4">
			<button
				v-for="page in totalPages"
				:key="page"
				class="btn"
				:class="{ 'btn-primary': page === currentPage, 'btn-outline': page !== currentPage }"
				@click="currentPage = page"
			>
				{{ page }}
			</button>
		</div>
	</div>
</template>
