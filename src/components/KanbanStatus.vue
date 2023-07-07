<template>
    <div class="kanban-status"
        @drop="onDrop($event, statusItem.statusId)"
        @dragenter.prevent
        @dragover.prevent
        >

        <div class="kanban-status-header" :style="{'background-color': statusItem.statusColor}">
            <h3 class="kanban-status-header__title">
                {{ statusItem.statusTitle }}
            </h3>
        </div>

        <div class="kanban-status-row">

            <KanbanCard
                v-for="item in cardItems.filter(x => x.status == statusItem.statusId)"
                :key="item.cardNumber"
                :cardItem="item"
                @click="openDetail(item)"
                draggable="true"
                @dragstart="startDrag($event, item)"
            />

        </div>
    </div>
</template>

<script>
import KanbanCard from './KanbanCard.vue';
export default {
    props: ['status', 'cards'],
    emits: ['openDetail', 'changeStatus'],

    setup (props, context) {
        
        function openDetail(item) {
            context.emit('openDetail', item)
        }

        function startDrag(evt, item) {
            evt.dataTransfer.dropEffect = 'move'
            evt.dataTransfer.effectAllowed = 'move'
            evt.dataTransfer.setData('itemId', item.cardNumber)
        }

        function onDrop(evt, statusId) {
            const itemId = evt.dataTransfer.getData('itemId')
            context.emit('changeStatus', itemId, statusId)
        }

        return {
            openDetail,
            statusItem: props.status,
            cardItems: props.cards,
            startDrag,
            onDrop,
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
    width: 200px;
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