<script setup>
import { computed, ref } from 'vue';
import { education } from '../lib/data.js';

// Pagination logic
const itemsPerPage = 4;
const currentPage = ref(1);
const totalPages = computed(() => Math.ceil(education.length / itemsPerPage));
const paginatedEducation = computed(() =>
	education.slice(
		(currentPage.value - 1) * itemsPerPage,
		currentPage.value * itemsPerPage
	)
);

</script>

<template>
	<div id="education" class="space-y-2 p-3 md:p-0">
		<h2 class="text-2xl font-semibold">Education</h2>

		<!-- Education cards -->
		<div class="space-y-4" v-for="edu in paginatedEducation">
			<div class="card border border-gray-400 bg-base-100">
				<div class="card-body">
					<h2 class="card-title">{{edu.title}}</h2>
					<p class="text-gray-300 font-semibold text-sm">{{edu.issuedBy}}</p>
					<p class="text-gray-300 font-light">{{edu.date}}</p>
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

<style>
</style>
