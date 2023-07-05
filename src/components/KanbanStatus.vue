<template>
    <div class="kanban-status">
        <div class="kanban-status-header">
            <h3 class="kanban-status-header__title">Статус</h3>
        </div>

        <div class="kanban-status-row">
            <KanbanCard @click="openDetail" />
            <KanbanCard @click="openDetail" />
            <KanbanCard @click="openDetail" />
        </div>
    </div>
</template>

<script>
import KanbanCard from './KanbanCard.vue';
export default {
    props: [],
    emits: ['openDetail'],

    setup (props, context) {
        
        function openDetail() {
            context.emit('openDetail')
        }

        return {
            openDetail
        }
    },
    components: {
        KanbanCard,
    }
}
</script>

<style lang="scss" scoped>

.kanban-status {
    padding: 8px;
    display: flex;
    flex-direction: column;
    gap: 12px;
}

.kanban-status-header{

    .kanban-status-header__title {
        border-radius: 20px;
        background: var(--rose, #FFDCE0);
        padding: 4px 12px;
    }

}

.kanban-status-row {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

</style>