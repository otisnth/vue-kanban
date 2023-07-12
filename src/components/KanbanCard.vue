<template>
    <div class="kanban-card">

        <div class="kanban-card__number">
            {{ cardFields.cardNumber }}
        </div>

        <h4 class="kanban-card__title">
            {{ cardFields.cardTitle }}
        </h4>

        <div class="kanban-card__property">

            <img class="kanban-card__icon" 
            :src='require(`../assets/images/${cardFields.type.typeIcon}`)'
            :alt="cardFields.type.typeTitle" 
            :title="cardFields.type.typeTitle"
            draggable="false"
            >

            <img class="kanban-card__icon" 
            :src='require(`../assets/images/${cardFields.priority.priorityIcon}`)'
            :alt="cardFields.priority.priorityTitle" 
            :title="cardFields.priority.priorityTitle"
            draggable="false"
            >

        </div>

        <div class="kanban-card__worker">

            <img class="kanban-card__avatar" 
            :src='require(`../assets/images/${cardFields.worker.workerAvatar}`)' 
            alt="Аватар"
            draggable="false"
            >

            <p class="kanban-card__worker-name">
                {{ cardFields.worker.workerName }}
            </p>

        </div>

    </div>
</template>

<script>
export default {
    props: ['cardItem'],
    // emits: [],
    setup (props) {

        return {
            cardFields: props.cardItem,
        }
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
    cursor: pointer;

    &__number {
        font-weight: 600;
        text-transform: uppercase;
        color: #5A5A65;
    }

    &__title {
        font-weight: 600;
    }

    &__property {
        display: flex;
        gap: 8px;
        padding: 4px 0;
        border-top: 1px solid #DDD;
        border-bottom: 1px solid #DDD;
    }

    &__icon {
        width: 20px;
    }

    &__worker {
        display: grid;
        grid-template-columns: min-content auto;
        gap: 8px;
        align-items: center;
    }

    &__avatar {
        width: 36px;
        border-radius: 50%;
    }

    &__worker-name {
        font-size: 14px;
        color: #5A5A65;
    }
}

</style>