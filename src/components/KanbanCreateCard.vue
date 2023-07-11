<template>
    <div class="kanban-create">
        <div class="kanban-create__header-line">
            <img src="@/assets/images/close.svg" 
                alt="Закрыть"
                @click="closeCreate">
        </div>
        <h4 class="kanban-create__title">Создание задачи</h4>
         
        <div class="kanban-create__input-wrap">
            <label for="cardNumber">Номер:</label>
            <input type="text" id="cardNumber">
        </div>

        <div class="kanban-create__input-wrap">
            <label for="cardTitle">Название:</label>
            <input type="text" id="cardTitle">
        </div>

        <div class="kanban-create__input-wrap">
            <label for="description">Название:</label>
            <textarea id="description" cols="30" rows="10"></textarea>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="type">Тип:</label>
            <select id="type">
                <option v-for="item in typesList"
                    :key="item.typeId"
                    :value="item">
                        {{ item.typeTitle }}
                </option>
            </select>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="priority">Приоритет:</label>
            <select id="priority">
                <option v-for="item in priorityList"
                    :key="item.priorityId"
                    :value="item">
                        {{ item.priorityTitle }}
                </option>
            </select>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="author">Автор:</label>
            <select id="author">
                <option v-for="item in workersList"
                    :key="item.workerId"
                    :value="item">
                        {{ item.workerName }}
                </option>
            </select>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="worker">Исполнитель:</label>
            <select id="worker">
                <option v-for="item in workersList"
                    :key="item.workerId"
                    :value="item">
                        {{ item.workerName }}
                </option>
            </select>
        </div>

    </div>
</template>

<script>
export default {
    props: ['workers', 'priority', 'types'],
    emits: ['closeCreate'],
    setup (props, context) {
        
        function closeCreate() {
            context.emit('closeCreate')
        }

        return {
            closeCreate,
            workersList: props.workers,
            priorityList: props.priority,
            typesList: props.types
        }
    }
}
</script>

<style lang="scss" scoped>

.kanban-create {
    position: absolute;
    backdrop-filter: blur(25px);
    z-index: 100;
    right: 0;
    top:0;
    width: 100%;
    height: 100%;
    padding: 40px;
    display: flex;
    flex-direction: column;
    gap: 20px;
    overflow-y: scroll;

    .kanban-create__header-line {
        display: flex;
        justify-content: end;
        
        img {
            width: 48px;
        }
    }
    .kanban-create__title {
        font-size: 36px;
        text-align: center;
    }

    .kanban-create__input-wrap{
        display: flex;
        flex-direction: column;
        gap: 4px;
    }

}

</style>