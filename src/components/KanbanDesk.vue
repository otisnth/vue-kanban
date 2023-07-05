<template>
    <div class="kanban-desk">

        <div class="kanban-desk-header">
            <h1 class="kanban-desk-header__title">Доска</h1>
            <p class="kanban-desk-header__description">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Cum a voluptates provident ut odit recusandae non sequi temporibus veniam doloremque cupiditate ratione, fugiat possimus culpa ipsam excepturi repellat reprehenderit iure.</p>
        </div>

        <div class="kanban-cards-wrap">
            <div class="kanban-status-grid">
                <KanbanStatus @openDetail="openDetail"/>
                <KanbanStatus @openDetail="openDetail"/>
                <KanbanStatus @openDetail="openDetail"/>
                <KanbanStatus @openDetail="openDetail"/>
                <KanbanStatus @openDetail="openDetail"/>
                <KanbanStatus @openDetail="openDetail"/>
                <KanbanStatus @openDetail="openDetail"/>
                <KanbanStatus @openDetail="openDetail"/>
                <KanbanStatus @openDetail="openDetail"/>
            </div>
            <KanbanCardDetail v-if="showDetail" @openDetail="openDetail" />
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
    // props: [],
    // emits: [],
    setup () {
        const showDetail = ref(false)

        function openDetail() {
            showDetail.value = !showDetail.value
        }

        return {
            showDetail,
            openDetail,
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
}

.kanban-status-grid {
    display: flex;
    background: #F8F8F8;
    border-radius: 12px;
    padding: 8px;
    box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
    overflow: scroll;
    height: 100%;
}

</style>