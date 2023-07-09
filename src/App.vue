<template>
    <div class="container">
        <KanbanDesk 
            :kanbanCards="kanbanCards"
            :kanbanWorkers="kanbanWorkers"
            :kanbanStatuses="kanbanStatuses"

        />
    </div>
</template>

<script>

import {
    ref,
} from 'vue'

import KanbanDesk from './components/KanbanDesk.vue';
import kanbanCardsJson from './assets/kanbanCards.json'
import kanbanWorkersJson from './assets/kanbanWorkers.json'
import kanbanStatusesJson from './assets/kanbanStatuses.json'

export default {
    setup () {
        const kanbanCards = ref(kanbanCardsJson)
        const kanbanWorkers = ref(kanbanWorkersJson)
        const kanbanStatuses = ref(kanbanStatusesJson)

        return {
            kanbanCards,
            kanbanWorkers,
            kanbanStatuses,
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
