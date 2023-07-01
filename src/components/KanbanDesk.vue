<template>
    <div class="kanban-desk">
        <h1>Доска</h1>
        <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Cum a voluptates provident ut odit recusandae non sequi temporibus veniam doloremque cupiditate ratione, fugiat possimus culpa ipsam excepturi repellat reprehenderit iure.</p>

        <div class="grid-kanban-status">
            <KanbanStatus />
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

.grid-kanban-status {
    display: flex;
    background: #F8F8F8;
    border-radius: 12px;
}

</style>