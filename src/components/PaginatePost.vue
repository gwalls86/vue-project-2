<script setup>
    defineProps(['inicioname','finname','maxlengthname']);    

    const emit = defineEmits(['prevname','nextname']);

</script>

<template>

    <div class="btn-group" role="group" aria-label="Basic example">
        <button 
            @click="emit('prevname')"
            type="button" 
            class="btn btn-outline-primary"
            :disabled="inicioname <= 0">
            Previous {{ inicioname }}
        </button>   

        <button
            @click="emit('nextname')" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="finname >= maxlengthname">
            Next {{ finname }}
        </button>
    </div>

</template>