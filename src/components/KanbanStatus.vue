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
            <input type="color" v-model="statusItem.statusColor" :id="statusItem.statusId">
            <label :for="statusItem.statusId">
                <img src="@/assets/images/palette.svg" alt="">
            </label>
        </div>

        <div class="kanban-status-row">

            <KanbanCard
                v-for="item in cardItems.filter(x => x.status == statusItem.statusId)"
                :key="item.cardNumber"
                :id="item.cardNumber"
                :cardItem="item"
                @click="openDetail(item)"
                draggable="true"
                @dragstart="startDrag($event, item)"
                @dragend="stopDrag($event, item)"
            />

        </div>
    </div>
</template>

<script>
import {
    ref
} from 'vue'
import KanbanCard from './KanbanCard.vue';
export default {
    props: ['status', 'cards'],
    emits: ['openDetail'],

    setup (props, context) {
        
        function openDetail(item) {
            context.emit('openDetail', item)
        }

        const cardItems = ref(props.cards)

        function startDrag(evt, item) {
            let draggedItem = document.querySelector(`#${item.cardNumber}`)
            setTimeout(() => {
                draggedItem.style.display = 'none'
            })

            evt.dataTransfer.dropEffect = 'none'
            evt.dataTransfer.effectAllowed = 'none'
            evt.dataTransfer.setData('itemId', item.cardNumber)
        }
        
        function stopDrag(evt, item) {
            let draggedItem = document.querySelector(`#${item.cardNumber}`)
            setTimeout(() => {
                draggedItem.style.display = 'flex'
            })
        }

        function onDrop(evt, statusId) {
            const itemId = evt.dataTransfer.getData('itemId')
            cardItems.value = cardItems.value.map(x => {
                if (x.cardNumber == itemId)
                    x.status = statusId
                return x
            })
        }

        return {
            openDetail,
            statusItem: props.status,
            cardItems,
            startDrag,
            stopDrag,
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
    display: flex;
    gap: 4px;
    justify-content: space-between;
    padding: 4px 12px;

    .kanban-status-header__title {
        
    }

    input {
        display: none;
        z-index: 0;
        opacity: 100;
        width: 18px;
        position: relative;
    }

    label {
        align-self: center;
    }

    img {
        width: 18px;
    }

}

.kanban-status-row {
    display: flex;
    flex-direction: column;
    gap: 8px;
    overflow: scroll;
}

</style>