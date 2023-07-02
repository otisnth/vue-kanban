<template>
    <div class="kanban-card">
        <div class="kanban-card__number">Number</div>
        <h4 class="kanban-card__title">Title</h4>
        <div class="kanban-card__type">Type</div>
        <div class="kanban-card__worker">Worker</div>
    </div>
</template>

<script>
export default {
    setup () {

        return {}
    }
}
</script>

<style lang="scss" scoped>

.kanban-card {
    padding: 16px;
    border-radius: 8px;
    border: 1px solid #DDD;
    background: #FFF;
    display: flex;
    flex-direction: column;
    gap: 6px;
    font-size: 16px;

    .kanban-card__number {
        text-transform: uppercase;
    }

    .kanban-card__title {
        font-weight: 600;
    }

    .kanban-card__type {
        
    }

    .kanban-card__worker {
        
    }
}

</style>