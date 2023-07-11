<template>
    <div class="kanban-desk">

        <div class="kanban-desk-header">
            <h1 class="kanban-desk-header__title">
                Доска
            </h1>

            <p class="kanban-desk-header__description">
                Lorem ipsum dolor sit, amet consectetur adipisicing elit. Cum a voluptates provident ut odit recusandae non sequi temporibus veniam doloremque cupiditate ratione, fugiat possimus culpa ipsam excepturi repellat reprehenderit iure.
            </p>

            <div class="kanban-desk-header__action-group">
                <button class="create-card"
                @click="openCreate">
                    Добавить карточку
                </button>
                <div class="delete-area"
                    @drop="deleteCard($event)"
                    @dragenter.prevent
                    @dragover.prevent>
                    Перетащите карточку для удаления
                </div>
            </div>
        </div>

        <div class="kanban-cards-wrap">

            <div class="kanban-status-grid">

                <KanbanStatus
                    v-for="item in statuses"
                    :key="item.statusId"
                    :status="item"
                    :cards="cards"
                    @openDetail="openDetail"
                />

            </div>

            <KanbanCardDetail 
                v-if="showDetail" 
                @closeDetail="closeDetail" 
                :item="detailCard"
                :workers="workers"
            />
            
            <KanbanCreateCard
                v-if="showCreate"
                :types="types"
                :priority="priority"
                :workers="workers"
                @closeCreate="closeCreate"
                @addCard="addCard"
            />
        </div>

    </div>
</template>

<script>
import {
    ref,
    computed
} from 'vue'

import KanbanStatus from './KanbanStatus.vue'
import KanbanCardDetail from './KanbanCardDetail.vue'
import KanbanCreateCard from './KanbanCreateCard.vue'

export default {
    props: ['kanbanCards', 'kanbanWorkers', 'kanbanStatuses', 'kanbanTypes', 'kanbanPriority'],
    emits: [],
    setup (props) {
        const showDetail = ref(false)
        const showCreate = ref(false)
        const detailCard = ref({})

        const cards = computed(() => {
            return props.kanbanCards
        })

        function openDetail(item) {
            detailCard.value = item
            showDetail.value = true
        }

        function closeDetail() {
            showDetail.value = false
        }

        function openCreate() {
            showDetail.value = false
            showCreate.value = true
        }

        function closeCreate() {
            showCreate.value = false
        }

        function addCard(newCard) {
            cards.value.push(newCard.value)
            showCreate.value = false
        }
        
        function deleteCard(evt) {
            const itemId = evt.dataTransfer.getData('itemId')
            cards.value.splice(0, cards.value.length, ...cards.value.filter(n => n.cardNumber != itemId))
        }

        return {
            showDetail,
            openDetail,
            closeDetail,
            statuses: props.kanbanStatuses,
            workers: props.kanbanWorkers,
            cards,
            types: props.kanbanTypes,
            priority: props.kanbanPriority,
            detailCard,
            closeCreate,
            openCreate,
            showCreate,
            addCard,
            deleteCard
        }
    },
    components: {
        KanbanStatus,
        KanbanCardDetail,
        KanbanCreateCard
    }
}
</script>

<style lang="scss" scoped>

.kanban-desk {
    display: flex;
    flex-direction: column;
    padding: 40px;
    gap: 20px;
    height: 100vh;
}

.kanban-desk-header {
    display: flex;
    flex-direction: column;
    gap: 8px;
    max-width: 50%;

    .kanban-desk-header__title {
        font-size: 32px;
        font-style: normal;
        font-weight: 700; 
        color: #212121; 
    }

    .kanban-desk-header__description {
        font-size: 14px;
        font-style: normal;
        font-weight: 400;
        color: #5A5A65; 
    }

    .kanban-desk-header__action-group{
        display: flex;
        gap: 15px;

        .create-card {
            padding: 8px;
            font: inherit;
            background-color: #44944A;
            border-color: transparent;
            border-radius: 4px;
            color: #fff;
        }

        .delete-area {
            border: 2px solid #AF2B1E;
            border-radius: 4px;
            padding: 8px;
        }
    }

}

.kanban-cards-wrap {
    height: 100%;
    position: relative;
    background: #F8F8F8;
    border-radius: 12px;
    box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
    overflow: hidden;
}

.kanban-status-grid {
    display: flex;
    padding: 8px;
    overflow-x: scroll;
    height: 100%;
}

</style>