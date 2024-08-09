<script setup>
    const props = defineProps(['tarefaPendente'])
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>
            Você possui {{ props.tarefaPendente }} tarefas pendentes
        </p>
    </header>
</template>