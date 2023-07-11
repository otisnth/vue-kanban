<template>
    <div class="container">
        <KanbanDesk 
            :kanbanCards="kanbanCards"
            :kanbanWorkers="kanbanWorkers"
            :kanbanStatuses="kanbanStatuses"
            :kanbanTypes="kanbanTypes"
            :kanbanPriority="kanbanPriority"

        />
    </div>
</template>

<script>

import {
    ref,
    watch,
    computed
} from 'vue'

import KanbanDesk from './components/KanbanDesk.vue';
// import kanbanCardsJson from './assets/kanbanCards.json'
import kanbanWorkersJson from './assets/kanbanWorkers.json'
import kanbanStatusesJson from './assets/kanbanStatuses.json'
import kanbanTypesJson from './assets/kanbanTypes.json'
import kanbanPriorityJson from './assets/kanbanPriority.json'

export default {
    setup () {
        // const kanbanCards = ref(kanbanCardsJson)
        const kanbanCards = ref(localStorage.getItem('cards') ? JSON.parse(localStorage.getItem('cards')) : [])
        const kanbanWorkers = ref(kanbanWorkersJson)
        const kanbanStatuses = ref(kanbanStatusesJson)
        const kanbanTypes = ref(kanbanTypesJson)
        const kanbanPriority = ref(kanbanPriorityJson)

        const cards = computed(() => {
            return kanbanCards.value
        })

        watch(cards.value, (newValue) => {
            localStorage.setItem('cards', JSON.stringify(newValue))
        })

        return {
            kanbanCards,
            kanbanWorkers,
            kanbanStatuses,
            kanbanPriority,
            kanbanTypes
        }
    },
    components: {
        KanbanDesk,
    }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    &::-webkit-scrollbar {
        width: 6px;
        height: 8px;
        background-color: transparent;
        border-radius: 3px;
    }

    &:hover::-webkit-scrollbar {
        background-color: #e7e7e7;
    }

    &:hover::-webkit-scrollbar-thumb {
        background-color: #5A5A65;
    }

    &::-webkit-scrollbar-thumb {
        background-color: transparent;
        border-radius: 3px;
    }
}

#app {
    font-family: 'Roboto', Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

.container {
    margin: 0 auto;
    max-width: 1440px;
}
</style>
