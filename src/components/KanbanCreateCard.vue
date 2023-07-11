<template>
    <div class="kanban-create">
        <div class="kanban-create__header-line">
            <img src="@/assets/images/close.svg" 
                alt="Закрыть"
                @click="closeCreate">
        </div>
        <h4 class="kanban-create__title">Создание задачи</h4>
         
        <div class="kanban-create__input-wrap">

        </div>

    </div>
</template>

<script>
export default {
    emits: ['closeCreate'],
    setup (props, context) {
        
        function closeCreate() {
            context.emit('closeCreate')
        }

        return {
            closeCreate,
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