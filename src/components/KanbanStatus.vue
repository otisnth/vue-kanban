<template>
    <div class="kanban-status"
        @drop="onDrop($event, statusItem.statusId)"
        @dragenter.prevent="enterRow($event)"
        @dragover.prevent
        @dragleave="leaveRow($event)"
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
                @dragstart.capture="startDrag($event, item)"
                @dragend="stopDrag($event, item)"
            />

        </div>
    </div>
</template>

<script>
import {
    computed
} from 'vue'
import KanbanCard from './KanbanCard.vue';
export default {
    props: ['status', 'cards'],
    emits: ['openDetail'],

    setup (props, context) {
        
        function openDetail(item) {
            context.emit('openDetail', item)
        }

        const cardItems = computed(() => {
            return props.cards
        })

        function startDrag(evt, item) {
            let draggedItem = document.querySelector(`#${item.cardNumber}`)
            setTimeout(() => {
                draggedItem.style.display = 'none'
            })
            console.log(draggedItem);

            console.log(evt);

            evt.dataTransfer.dropEffect = 'move'
            evt.dataTransfer.effectAllowed = 'move'
            evt.dataTransfer.setData('itemId', item.cardNumber)
        }
        
        function stopDrag(evt, item) {
            let draggedItem = document.querySelector(`#${item.cardNumber}`)
            if (draggedItem)
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
            evt.target.classList.remove("kanban-status_select")
        }

        function enterRow(evt) {
            evt.target.classList.add("kanban-status_select")
        }

        function leaveRow(evt) {
            evt.target.classList.remove("kanban-status_select")
        }

        return {
            openDetail,
            statusItem: props.status,
            cardItems,
            startDrag,
            stopDrag,
            onDrop,
            enterRow,
            leaveRow
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
    border: 2px solid transparent;
    border-radius: 8px;

    &_select {
        background-color: #e7e7e7;
    }
}

.kanban-status-header {
    width: 200px;
    border-radius: 20px;
    background: #fff;
    display: flex;
    gap: 4px;
    justify-content: space-between;
    padding: 4px 12px;

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
    overflow-y: scroll;
    overflow-x: hidden;
}

</style>