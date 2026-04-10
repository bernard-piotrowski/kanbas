<script setup>

///////////////////////////////////////////////
// IDs to be used for the respective DOM elements in the template
///////////////////////////////////////////////

const BUTTON_TOGGLE_MODAL_ID = 'buttonToggleModal' // for the button that opens the modal

const emit = defineEmits(['open-modal']);

defineProps({
    title: {
        type: String,
        required: true
    }
});
</script>

<template>
    <nav class="navbar bg-light">
        <div class="container-fluid">
            <span class="navbar-brand mb-0 h1">
                <img src="../assets/logo.svg" alt="Logo" width="24" height="24" class="d-inline-block align-text-top">
                {{ title }}
            </span>
             <button 
             :id="BUTTON_TOGGLE_MODAL_ID" 
             class="btn btn-primary" 
             data-bs-toggle="modal"
             data-bs-target="#modalRoot"
             @click="emit('open-modal')" 
             >
             Create new task
            </button>
        </div>
    </nav>
</template>