<script setup>
import {ref, defineProps, defineEmits} from 'vue';

const props = defineProps({ tags: Array, columns: Array });
console.log(props.tags);
const emit = defineEmits(['close', 'submit']);

const selectedColumn = ref('');
const taskTitle = ref('');
const taskDescription = ref('');
const selectTags = ref([]);
///////////////////////////////////////////////
// IDs to be used for the respective DOM elements in the template
///////////////////////////////////////////////

const MODAL_ID = 'modalRoot' // for the modal's root element
const MODAL_SELECT_COLUMN_ID = 'modalSelectColumn' // for the selector in the modal's header
const MODAL_BUTTON_X_ID = 'modalButtonX'
const MODAL_INPUT_TITLE_ID = 'modalInputTitle' // for the input where users enter the task's title
const MODAL_HELPER_TITLE_ID = 'modalHelperTitle' // for the helper showing the length of entered title
const MODAL_INPUT_TEXT_ID = 'modalInputText' // for the textarea where users enter the task's description
const MODAL_DROPDOWN_TRIGGER_ID = 'modalDropdownTrigger' // for the button that toggles the tag selection dropdown
const MODAL_DROPDOWN_MENU_ID = 'modalDropdownMenu' // for the root element of the tag selection dropdown's menu
const MODAL_CHECKBOX_BASE_ID = 'modalCheckbox' // base string for the checkboxes in the dropdown, concatenate with the respective tag's name
const MODAL_BUTTON_CANCEL = 'modalButtonCancel' // for the modal's cancel button
const MODAL_BUTTON_SUBMIT = 'modalButtonSubmit' // for the modal's submit button


const resetFormular = () => {
    selectedColumn.value = '';
    taskTitle.value = '';
    taskDescription.value = '';
    selectTags.value = [];
};
const closeModal = () => {
    resetFormular();
    emit('close');
};
const submitTask = () => {
    if (!taskTitle.value.trim()) return;
    emit('submit', {
        column: selectedColumn.value,
        title: taskTitle.value.trim(),
        text: taskDescription.value.trim(),
        tags: [...selectTags.value]
    });
    resetFormular();
};
</script>

<template>
    <div :id="MODAL_ID" class="modal fade" tabindex="-1">
         <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Create New Task</h5>
                    <button type="button" class="btn-close" :id="MODAL_BUTTON_X_ID" @click="closeModal"></button>
                </div>
                <div class="modal-body">
                    <!-- Column Select -->
                    <div class="mb-3">
                        <label for="modalSelectColumn" class="form-label">Select a Column</label>
                        <select :id="MODAL_SELECT_COLUMN_ID" class="form-select" v-model="selectedColumn">
                            <option disabled value="">Select a column</option>
                            <option v-for="col in props.columns" :key="col.id" :value="col.name">
                                {{ col.name }}
                            </option>
                        </select>
                    </div>
                    <!-- task title -->
                    <div class="mb-3">
                        <label for="modalInputTitle" class="form-label">Task Title</label>
                        <input type="text" class="form-control" :id="MODAL_INPUT_TITLE_ID" v-model="taskTitle" maxlength="50"/>
                        <div :id="MODAL_HELPER_TITLE_ID" class="form-text">{{ taskTitle.length }}/50</div>
                    </div>
                    <!-- task description -->
                     <div class="mb-3">
                        <label for="modalInputText" class="form-label">Task Description</label>
                        <textarea class="form-control" :id="MODAL_INPUT_TEXT_ID" v-model="taskDescription" rows="4"></textarea>
                     </div>
                     <!-- Tag selection -->
                      <div class="mb-3">
                        <button class="btn btn-secondary" type="button" :id="MODAL_DROPDOWN_TRIGGER_ID" data-bs-toggle="dropdown" aria-expanded="false">
                            chose Tags
                        </button>
                        <ul class="dropdown-menu p-3" :id="MODAL_DROPDOWN_MENU_ID">
                            <li v-for="tag in tags" :key="tag.name">
                                <div class="form-check">
                                    <input class="form-check-input" type="checkbox" :id="`${MODAL_CHECKBOX_BASE_ID}${tag}`" :value="tag" v-model="selectTags"/>
                                    <label class="form-check-lable" :for="`${MODAL_CHECKBOX_BASE_ID}${tag}`">{{ tag }}</label>
                                </div>
                            </li>
                        </ul>
                      </div>
                </div>
                <!-- Button -->
                 <button type="button" class="btn btn-secondary rounded-0" :id="MODAL_BUTTON_CANCEL" @click="closeModal">Cancel</button>
                 <button type="button" class="btn btn-primary rounded-top-0" :id="MODAL_BUTTON_SUBMIT" @click="submitTask">Safe</button>
            </div>
         </div>
    </div>
</template>
