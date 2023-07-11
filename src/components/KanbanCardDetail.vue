<template>
    <div class="kanban-card-detail">

        <div class="detail-header">

            <img class="detail-header__close" 
                src="@/assets/images/left-arrow.svg" 
                alt="Назад" 
                @click="closeDetail"
            >
            
            <p class="detail-header__number">
                {{ detailFields.cardNumber }}
            </p>

            <div class="detail-header__title">
                <input type="text" 
                    v-model="detailFields.cardTitle"
                    :disabled="!changeTitle"
                >
                <img 
                    src="@/assets/images/pen.svg" 
                    alt="Изменить"
                    @click="()=>{changeTitle = !changeTitle}"
                >
            </div>

        </div>

        <div class="detail-container">

            <div class="detail-info">

                <p class="detail-title">
                    Тип:
                </p>

                <div class="detail-info__item">

                    <img 
                        :src='require(`../assets/images/${detailFields.type.typeIcon}`)'
                        :alt="detailFields.type.typeTitle" 
                        class="detail-info__icon"
                    >
                    <p class="detail-info__text">
                        {{ detailFields.type.typeTitle }}
                    </p>

                </div>

            </div>

            <div class="detail-info">

                <p class="detail-title">
                    Приоритет:
                </p>

                <div class="detail-info__item">

                    <img 
                        :src='require(`../assets/images/${detailFields.priority.priorityIcon}`)'
                        :alt="detailFields.priority.priorityTitle" 
                        class="detail-info__icon"
                    >

                    <p class="detail-info__text">
                        {{ detailFields.priority.priorityTitle }}
                    </p>

                </div>

            </div>

            <div class="detail-description">
                <textarea rows="2"
                    v-model="detailFields.description"
                    :disabled="!changeDescription"
                    placeholder="Описание"
                    ref="decriptionField"
                ></textarea>
                <img 
                    src="@/assets/images/pen.svg" 
                    alt="Изменить"
                    @click="()=>{changeDescription = !changeDescription}"
                >
            </div>

            <div class="detail-user">

                <p class="detail-title">
                    Автор: 
                </p>

                <div class="detail-user__item">

                    <img 
                        :src='require(`../assets/images/${detailFields.author.workerAvatar}`)' 
                        alt="Аватар" 
                        class="detail-user__avatar"
                    >

                    <p class="detail-user__author">
                        {{ detailFields.author.workerName }}
                    </p>

                </div>

            </div>

            <div class="detail-user">

                <p class="detail-title">
                    Исполнитель: 
                </p>

                <div class="detail-user__item">

                    <img 
                        :src='require(`../assets/images/${detailFields.worker.workerAvatar}`)' 
                        alt="Аватар" 
                        class="detail-user__avatar"
                    >

                    <select class="detail-user__worker" v-model="detailFields.worker">
                        <option v-for="item in workersList"
                            :key="item.workerId"
                            :value="item">
                                {{ item.workerName }}
                        </option>
                    </select>

                </div>

            </div>

            <div class="detail-date">

                <p class="detail-title">
                    Дата создания: 
                </p>

                <span class="detail-date__value">
                    {{ detailFields.createDate }}
                </span>

            </div>

            <div class="detail-date">

                <p class="detail-title">
                    Дата обновления: 
                </p>

                <span class="detail-date__value">
                    {{ detailFields.updateDate }}
                </span>

            </div>

        </div>

    </div>
</template>

<script>
import {
    ref,
    computed,
    watch,
    onRenderTracked,
    onUpdated,
    onMounted
} from 'vue'

export default {
    props: ['item', 'workers'],
    emits: ['openDetail'],
    setup (props, context) {

        const changeTitle = ref(false)
        const changeDescription = ref(false)
        const decriptionField = ref(null)

        const workersList = ref(props.workers)

        function closeDetail() {
            context.emit('closeDetail')
        }

        onRenderTracked(() => {
            changeTitle.value = false
            changeDescription.value = false
        })

        onUpdated(()=>{
            decriptionField.value.style.height = "auto"
            decriptionField.value.style.height = decriptionField.value.scrollHeight + "px"
        })

        onMounted(()=>{
            decriptionField.value.style.height = "auto"
            decriptionField.value.style.height = decriptionField.value.scrollHeight + "px"
        })

        const detailFields = computed(() => {
            return props.item
        })

        watch(
            () => [detailFields.value.worker, detailFields.value],
            (newValues, oldValues) => {
                if (newValues[1].cardNumber == oldValues[1].cardNumber) {
                    detailFields.value.updateDate = new Date().toLocaleDateString()
                }
            }
        )

        watch(
            () => [detailFields.value.cardTitle, detailFields.value],
            (newValues, oldValues) => {
                if (newValues[1].cardNumber == oldValues[1].cardNumber) {
                    detailFields.value.updateDate = new Date().toLocaleDateString()
                }
            }
        )

        watch(
            () => [detailFields.value.description, detailFields.value],
            (newValues, oldValues) => {
                if (newValues[1].cardNumber == oldValues[1].cardNumber) {
                    detailFields.value.updateDate = new Date().toLocaleDateString()
                }
            }
        )

        return {
            changeTitle,
            changeDescription,
            closeDetail,
            detailFields,
            workersList,
            decriptionField
        }
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
    overflow-y: scroll;
    overflow-x: hidden;
    padding: 40px;
    display: flex;
    flex-direction: column;
    gap: 25px;

    .detail-header {
        display: flex;
        flex-direction: column;
        gap: 10px;
        font-size: 24px;

        .detail-header__number {
            color: #5A5A65; 
        }

        .detail-header__title {
            display: flex;
            justify-content: space-between;
            align-items: center;
            input {
                font-size: 24px;
                font-weight: 700;
                border: 1px solid transparent;
                background-color: transparent;
                border-bottom: 1px solid #5A5A65;
            }

            input:disabled {
                color: #000;
                border: 1px solid transparent;
            }

            input:focus {
                outline: none;
            }

            img {
                width: 18px;
            }

        }

        .detail-header__close {
            width: 25px;
        }
    }

    .detail-container {
        display: flex;
        flex-direction: column;
        gap: 15px;

        .detail-title {
            color: #5A5A65;
        }

        .detail-info {
            display: flex;
            flex-direction: column;
            gap: 8px;

            .detail-info__item {
                display: flex;
                gap: 8px;
                padding-left: 10px;
                align-items: center;
            }
            .detail-info__icon {
                width: 20px;
            }

            .detail-info__text {

            }
        }

        .detail-description {
            display: flex;
            justify-content: space-between;
            align-items: start;
            textarea {
                width: 100%;
                font: inherit;
                border: 1px solid transparent;
                background-color: transparent;
                resize: none;
                overflow: hidden;
                border-bottom: 1px solid #5A5A65;
            }

            textarea:disabled {
                color: #000;
                border: 1px solid transparent;
            }

            textarea:focus {
                outline: none;
            }

            img {
                width: 18px;
            }
        }


        .detail-user {
            display: flex;
            flex-direction: column;
            gap: 8px;
            .detail-user__item {
                display: flex;
                gap: 16px;
                align-items: center;
            }
            .detail-user__avatar {
                    width: 36px;
                    border-radius: 50%;
            }
            .detail-user__author {
                
            }
            .detail-user__worker {
                background-color: transparent;
                border: none;
                font-size: 16px;
            }

        }

        .detail-date {
            display: flex;
            gap: 8px;
            align-items: center;
            .detail-date__value {

            }
        }
    }

}

</style>