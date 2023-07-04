<template>
    <div class="kanban-card-detail">

        <div class="detail-header">
            <p class="detail-header__number">N-930</p>
            <h4 class="detail-header__title">Title task</h4>
        </div>

        <div class="detail-container">

            <div class="detail-info">
                <p class="detail-info__title">Тип:</p>
                <div class="detail-info__item">
                    <img src="@/assets/images/bug.svg" alt="" class="detail-info__icon">
                    <p class="detail-info__text">Дефект</p>
                </div>
            </div>

            <div class="detail-info">
                <p class="detail-info__title">Приоритет:</p>
                <div class="detail-info__item">
                    <img src="@/assets/images/prio-low.svg" alt="" class="detail-info__icon">
                    <p class="detail-info__text">Низкий приоритет</p>
                </div>
            </div>

            <p class="detail-description">Lorem ipsum dolor sit amet consectetur adipisicing elit. Magnam deleniti eos aliquid cupiditate corporis hic commodi, dolore vitae necessitatibus voluptas veritatis corrupti, quidem totam reiciendis! Quasi facilis velit accusamus dolore.</p>

            <div class="detail-user">
                <p class="detail-user__title">Автор: </p>
                <div class="detail-author">
                    <img src="@/assets/images/avatar2.png" alt="" class="detail-author__avatar">
                    <p class="detail-author__name">Lastname Firstname</p>
                </div>
            </div>

            <div class="detail-user">
                <p class="detail-user__title">Исполнитель: </p>
                <div class="detail-worker">
                    <img src="@/assets/images/avatar1.png" alt="" class="detail-worker__avatar">
                    <select class="detail-worker__name">
                        <option value="">Lastname Firstname</option>
                    </select>
                </div>
            </div>

            <div class="detail-date">
                <p class="detail-date__title">Дата создания: </p>
                <input type="date" name="" id="" class="detail-date__value" value="2020-01-20">
            </div>

            <div class="detail-date">
                <p class="detail-date__title">Дата обновления: </p>
                <input type="date" name="" id="" class="detail-date__value" value="2020-01-25">
            </div>

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

.kanban-card-detail {
    position: absolute;
    backdrop-filter: blur(25px);
    border-radius: 12px;
    border: 2px solid #e7e7e7;
    height: 100%;
    width: 35%;
    z-index: 100;
    right: 0;
    top:0;
    overflow: scroll;
    padding: 40px;

    .detail-header {
        display: flex;
        flex-direction: column;
        gap: 10px;
    }

    .detail-container {
        display: flex;
        flex-direction: column;
        gap: 15px;

        .detail-info {
            display: flex;
            flex-direction: column;
            gap: 8px;

            .detail-info__item {
                display: flex;
                gap: 8px;
            }
            .detail-info__icon {
                width: 20px;
            }
        }


        .detail-user {
            display: flex;
            flex-direction: column;
            gap: 8px;

            .detail-worker {
                display: flex;
                gap: 8px;
                .detail-worker__avatar {
                    width: 36px;
                    border-radius: 50%;
                }
            }

            .detail-author {
                display: flex;
                gap: 8px;
                .detail-author__avatar {
                    width: 36px;
                    border-radius: 50%;
                }
            }
        }
    }

}

</style>