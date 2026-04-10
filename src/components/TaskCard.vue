<script setup>
import { ref } from 'vue';
import Tag from './Tag.vue';
const props = defineProps(['title', 'text', 'tags', 'id']);
const emit = defineEmits(['delete']);

const isExpanded = ref(false);
const toggleDescription = () => {
    isExpanded.value = !isExpanded.value;
};
</script>

<template>
    <div class="card mb-3 shadow-sm border-0">
        <div class="card-body">
            <h5 class="card-title mb-2">{{ title }} </h5>

            <p class="card-text text-muted mb-3 card-description"
            :class="{ 'expanded': isExpanded }"
            @click="toggleDescription">
            {{ text }}
            </p>
            <div class="d-flex flex-wrap gap-1">
                <Tag v-for="tag in tags" 
                :key="tag" 
                :tag="tag"
                />
				<button type="button" class="btn-close" aria-label="Close" @click.stop="emit('delete', props.id)"></button>
            </div>
        </div>
    </div>
</template>
<style scoped>
.card-description {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    cursor: pointer;
}
.card-description.expanded {
    white-space: normal;
    overflow: visivle;
    text-overflow: unset;
}
</style>