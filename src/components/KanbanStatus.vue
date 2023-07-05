<template>
    <div class="kanban-status">

        <div class="kanban-status-header" :style="{'background-color': statusItem.statusColor}">
            <h3 class="kanban-status-header__title">
                {{ statusItem.statusTitle }}
            </h3>
        </div>

        <div class="kanban-status-row">

            <KanbanCard
            v-for="(item, index) in statusItem.cards"
            :key="index"
            :cardItem="item"
            @click="openDetail(item)" 
            />

        </div>
    </div>
</template>

<script>
import KanbanCard from './KanbanCard.vue';
export default {
    props: ['statusItems'],
    emits: ['openDetail'],

    setup (props, context) {
        
        function openDetail(item) {
            context.emit('openDetail', item)
        }

        return {
            openDetail,
            statusItem: props.statusItems,
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

.kanban-status-header {
    border-radius: 20px;
    background: #fff;

    .kanban-status-header__title {
        padding: 4px 12px;
    }

}

.kanban-status-row {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

</style>