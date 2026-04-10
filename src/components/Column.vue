<script setup>
	import TaskCard from './TaskCard.vue';
	const props = defineProps(['name', 'tasks']);
	const emit = defineEmits(['delete']);
	const deleteTask = (taskId) => {
		emit('delete',{
			columnName: props.name,
			taskId
		})
	}
</script>

<template>
    <div class="p-4 bg-transparent">
        <h4 class="pt-3">{{ name }}</h4>
        <div v-for="task in tasks" :key="task.id">
            <TaskCard :title="task.title" :text="task.text" :tags="task.tags" :id="task.id" @delete="deleteTask"></TaskCard> 
        </div>
    </div>
</template>