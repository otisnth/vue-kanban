<template>
    <div class="container">
        <KanbanDesk />
    </div>
</template>

<script>

import KanbanDesk from './components/KanbanDesk.vue';

export default {
    setup () {
        

        return {}
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
