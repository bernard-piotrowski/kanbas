<script setup>
	import Column from './Column.vue';

	defineProps({
		columns: {
            type: Array,
			required: true
		}
	});
	const emit = defineEmits(['delete']);
</script>

<template>
	<div class="container">
		<div class="row">
			<div 
			v-for="column in columns"
			:key="column.id"
			class="col-12 col-md-6 col-lg-4 mb-3"
			>
            <Column :name="column.name" :tasks="column.tasks" @delete="emit('delete', $event)"/>
			</div>
		</div>
	</div>
</template>
