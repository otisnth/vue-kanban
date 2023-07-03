<template>
    <div class="kanban-card">
        <div class="kanban-card__number">N-930</div>
        <h4 class="kanban-card__title">Title task</h4>
        <div class="kanban-card__property">
            <img class="kanban-card__icon" src="@/assets/images/bug.svg" alt="Дефект" title="Дефект">
            <img class="kanban-card__icon" src="@/assets/images/prio-low.svg" alt="Низкий приоритет" title="Низкий приоритет">
        </div>
        <div class="kanban-card__worker">
            <img class="kanban-card__avatar" src="@/assets/images/avatar1.png" alt="Аватар">
            <p class="kanban-card__worker-name">Lastname Firstname</p>
        </div>
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
    width: 200px;
    padding: 16px;
    border-radius: 8px;
    border: 1px solid #DDD;
    background: #FFF;
    display: flex;
    flex-direction: column;
    gap: 6px;
    font-size: 16px;

    .kanban-card__number {
        font-weight: 600;
        text-transform: uppercase;
        color: #5A5A65;
    }

    .kanban-card__title {
        font-weight: 600;
    }

    .kanban-card__property {
        display: flex;
        gap: 8px;
        padding: 4px 0;
        border-top: 1px solid #DDD;
        border-bottom: 1px solid #DDD;
    }

    .kanban-card__icon {
        width: 20px;
    }

    .kanban-card__worker {
        display: grid;
        grid-template-columns: min-content auto;
        gap: 8px;
        align-items: center;
    }

    .kanban-card__avatar {
        width: 36px;
        border-radius: 50%;
    }

    .kanban-card__worker-name {
        font-size: 14px;
        color: #5A5A65;
    }
}

</style>