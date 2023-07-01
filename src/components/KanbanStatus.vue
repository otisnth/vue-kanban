<template>
    <div class="kanban-status">
        <h3>Статус</h3>
        <KanbanCard />
    </div>
</template>

<script>
import KanbanCard from './KanbanCard.vue';
export default {
    setup () {
        

        return {}
    },
    components: {
        KanbanCard
    }
}
</script>

<style lang="scss" scoped>

.kanban-status {
    padding: 8px;
    display: flex;
    flex-direction: column;
    gap: 8px;
}

</style>