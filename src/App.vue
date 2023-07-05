<template>
    <div class="container">
        <KanbanDesk :kanbanItems="kanbanItems"/>
    </div>
</template>

<script>

import {
    ref,
} from 'vue'

import KanbanDesk from './components/KanbanDesk.vue';
import kanbanItemsJson from './assets/kanbanItems.json'

export default {
    setup () {
        const kanbanItems = ref(kanbanItemsJson)

        return {
            kanbanItems,
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
