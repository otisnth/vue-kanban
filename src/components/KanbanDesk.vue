<template>
    <div class="kanban-desk">

        <div class="kanban-desk-header">
            <h1 class="kanban-desk-header__title">Доска</h1>
            <p class="kanban-desk-header__description">Lorem ipsum dolor sit, amet consectetur adipisicing elit. Cum a voluptates provident ut odit recusandae non sequi temporibus veniam doloremque cupiditate ratione, fugiat possimus culpa ipsam excepturi repellat reprehenderit iure.</p>
        </div>

        <div class="kanban-status-grid">
            <KanbanStatus />
            <KanbanStatus />
            <KanbanStatus />
        </div>

    </div>
</template>

<script>
import KanbanStatus from './KanbanStatus.vue'

export default {
    setup () {
        

        return {}
    },
    components: {
        KanbanStatus
    }
}
</script>

<style lang="scss" scoped>

.kanban-desk {
    display: flex;
    flex-direction: column;
    padding: 40px;
    gap: 20px;
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

.kanban-status-grid {
    display: flex;
    background: #F8F8F8;
    border-radius: 12px;
    padding: 8px;
    box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
}

</style>