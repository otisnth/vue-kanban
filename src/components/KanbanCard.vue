<template>
    <div class="kanban-card">
        <div class="kanban-card__number">N-930</div>
        <h4 class="kanban-card__title">Title</h4>
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
        text-transform: uppercase;
    }

    .kanban-card__title {
        font-weight: 600;
    }

    .kanban-card__property {
        display: flex;
        gap: 4px;
    }

    .kanban-card__icon {
        width: 18px;
    }

    .kanban-card__worker {
        display: flex;
        gap: 4px;
    }

    .kanban-card__avatar {
        width: 18px;
        border-radius: 50%;
    }
}

</style>