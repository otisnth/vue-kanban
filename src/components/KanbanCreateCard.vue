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
            <input type="text" 
                id="cardNumber"
                v-model="createdTask.cardNumber">
            <span class="validation-error">{{ validationErrors.number }}</span>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="cardTitle">Название:</label>
            <input type="text" 
                id="cardTitle"
                v-model="createdTask.cardTitle">
            <span class="validation-error">{{ validationErrors.title }}</span>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="description">Описание:</label>
            <textarea id="description"
                rows="1"
                @keydown="changeHeightTextarea($event)"
                v-model="createdTask.description">
            </textarea>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="type">Тип:</label>

            <div class="select-wrap">
                <img v-if="createdTask.type"
                class="icon"
                :src='require(`../assets/images/${createdTask.type.typeIcon}`)'>
                <div class="icon" v-else></div>
                <select id="type"
                    v-model="createdTask.type">
                    <option v-for="item in typesList"
                        :key="item.typeId"
                        :value="item">
                            {{ item.typeTitle }}
                    </option>
                </select>
            </div>
            <span class="validation-error">{{ validationErrors.type }}</span>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="priority">Приоритет:</label>
            
            <div class="select-wrap">
                <img v-if="createdTask.priority"
                class="icon"
                :src='require(`../assets/images/${createdTask.priority.priorityIcon}`)'>
                <div class="icon" v-else></div>
                <select id="priority"
                    v-model="createdTask.priority">
                    <option v-for="item in priorityList"
                        :key="item.priorityId"
                        :value="item">
                            {{ item.priorityTitle }}
                    </option>
                </select>
            </div>
            <span class="validation-error">{{ validationErrors.priority }}</span>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="author">Автор:</label>
            <div class="select-wrap">
                <img v-if="createdTask.author"
                class="avatar"
                :src='require(`../assets/images/${createdTask.author.workerAvatar}`)'>
                <div class="avatar" v-else></div>
                <select id="author"
                    v-model="createdTask.author">
                    <option v-for="item in workersList"
                        :key="item.workerId"
                        :value="item">
                            {{ item.workerName }}
                    </option>
                </select>
            </div>
            <span class="validation-error">{{ validationErrors.author }}</span>
        </div>

        <div class="kanban-create__input-wrap">
            <label for="worker">Исполнитель:</label>
            <div class="select-wrap">
                <img v-if="createdTask.worker"
                class="avatar"
                :src='require(`../assets/images/${createdTask.worker.workerAvatar}`)'>
                <div class="avatar" v-else></div>
                <select id="worker"
                    v-model="createdTask.worker">
                    <option v-for="item in workersList"
                        :key="item.workerId"
                        :value="item">
                            {{ item.workerName }}
                    </option>
                </select>
            </div>
            <span class="validation-error">{{ validationErrors.worker }}</span>
        </div>

        <button class="kanban-create__submit"
            @click="createCard">
            Создать
        </button>

    </div>
</template>

<script>
import {
    ref,
    watch
} from 'vue'

export default {
    props: ['workers', 'priority', 'types', 'cards'],
    emits: ['closeCreate', 'addCard'],
    setup (props, context) {
        const decriptionField = ref(null)
        const createdTask = ref({
            'cardNumber': "",
            'cardTitle': "",
            'description': "",
            'type': null,
            'priority': null,
            'worker': null,
            'author': null,
            'status': 0,
            'updateDate': "",
            'createDate': ""
        })

        const validationErrors = ref({
            'title': "Введите название!",
            'number': "",
            'type': "",
            'priority': "",
            'author': "",
            'worker': ""
        })

        const cardsList = ref(props.cards)
        
        function closeCreate() {
            context.emit('closeCreate')
        }

        watch(createdTask.value, (newValues) => {
            if (!newValues.type)
                validationErrors.value.type = "Выберите тип!"
            else
                validationErrors.value.type = ""
            
            if (!newValues.priority)
                validationErrors.value.priority = "Выберите приоритет!"
            else
                validationErrors.value.priority = ""

            if (!newValues.author)
                validationErrors.value.author = "Выберите автора!"
            else
                validationErrors.value.author = ""
            
            if (!newValues.worker)
                validationErrors.value.worker = "Выберите исполнителя!"
            else
                validationErrors.value.worker = ""
            
            if (!newValues.cardTitle)
                validationErrors.value.title = "Введите название!"
            else
                validationErrors.value.title = ""
            
            let pattern = /^[A-Za-z]*[-]\d+$/
            if (!pattern.test(newValues.cardNumber))
                validationErrors.value.number = "Номер должен иметь формат: символы латинского алфавита - цифры"
            else if (cardsList.value.find(card => card.cardNumber == newValues.cardNumber.toUpperCase()))
                validationErrors.value.number = "Номер должен быть уникальным"
            else
                validationErrors.value.number = ""

        })

        function createCard() {
            createdTask.value.createDate = new Date().toLocaleDateString()
            for (let key in validationErrors.value) {
                if (validationErrors.value[key]) return;
            }
            context.emit('addCard', createdTask)
        }

        function changeHeightTextarea(evt) {
            evt.target.style.height = "auto"
            evt.target.style.height = evt.target.scrollHeight + "px"
        }

        return {
            closeCreate,
            workersList: props.workers,
            priorityList: props.priority,
            typesList: props.types,
            decriptionField,
            changeHeightTextarea,
            createdTask,
            createCard,
            validationErrors
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
    top: 0;
    width: 100%;
    height: 100%;
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 10px;
    overflow-y: scroll;
    align-items: center;

    .kanban-create__header-line {
        display: flex;
        align-self: end;
        
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
        gap: 8px;
        width: 50%;

        label {
            font-size: 18px;
            font-weight: bold;
        }

        input {
                font: inherit;
                border: 1px solid transparent;
                background-color: transparent;
                border-bottom: 1px solid #5A5A65;
            }

        input:focus {
            outline: none;
        }

        textarea {
                width: 100%;
                font: inherit;
                border: 1px solid transparent;
                background-color: transparent;
                resize: none;
                overflow: hidden;
                border-bottom: 1px solid #5A5A65;
        }

        textarea:focus {
            outline: none;
        }

        .validation-error {
            font-size: 14px;
            color: red;
            height: 1rem;
        }

        .select-wrap {
            display: flex;
            gap: 8px;

            .icon {
                width: 20px;
            }

            .avatar {
                width: 36px;
                height: 36px;
                border-radius: 50%;
            }

            select {
                width: 100%;
                background-color: transparent;
                border: none;
                font: inherit;
                border-bottom: 1px solid #5A5A65;
            }

            select:focus {
                outline: none;
            }
        }


    }

    .kanban-create__submit {
        padding: 8px;
        font: inherit;
        background-color: #44944A;
        border-color: transparent;
        border-radius: 4px;
        color: #fff;
    }

}

</style>