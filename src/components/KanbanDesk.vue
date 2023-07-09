<template>
    <div class="kanban-desk">

        <div class="kanban-desk-header">
            <h1 class="kanban-desk-header__title">
                Доска
            </h1>

            <p class="kanban-desk-header__description">
                Lorem ipsum dolor sit, amet consectetur adipisicing elit. Cum a voluptates provident ut odit recusandae non sequi temporibus veniam doloremque cupiditate ratione, fugiat possimus culpa ipsam excepturi repellat reprehenderit iure.
            </p>
        </div>

        <div class="kanban-cards-wrap">

            <div class="kanban-status-grid">

                <KanbanStatus
                    v-for="item in statuses"
                    :key="item.statusId"
                    :status="item"
                    :cards="cards"
                    @openDetail="openDetail"
                    @changeStatus="changeStatus"
                />

            </div>

            <KanbanCardDetail 
                v-if="showDetail" 
                @closeDetail="closeDetail" 
                :item="detailCard"
                :workers="workers"
            />
            
        </div>

    </div>
</template>

<script>
import {
    ref,
} from 'vue'

import KanbanStatus from './KanbanStatus.vue'
import KanbanCardDetail from './KanbanCardDetail.vue'

export default {
    props: ['kanbanCards', 'kanbanWorkers', 'kanbanStatuses'],
    emits: ['changeStatus'],
    setup (props, context) {
        const showDetail = ref(false)
        const detailCard = ref({})

        function openDetail(item) {
            detailCard.value = item
            showDetail.value = true
        }

        function closeDetail() {
            showDetail.value = false
        }

        function changeStatus(itemId, statusId) {
            context.emit('changeStatus', itemId, statusId)
        }
        
        return {
            showDetail,
            openDetail,
            closeDetail,
            statuses: props.kanbanStatuses,
            workers: props.kanbanWorkers,
            cards: props.kanbanCards,
            detailCard,
            changeStatus
        }
    },
    components: {
        KanbanStatus,
        KanbanCardDetail
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
    // overflow: scroll;
    height: 100%;
}

</style>