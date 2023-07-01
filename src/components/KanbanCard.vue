<template>
    <div class="kanban-card">
        <span>Number</span>
        <h4>Title</h4>
        <div>Type</div>
        <div>Worker</div>

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

.kanban-card {
    padding: 16px;
    border-radius: 8px;
    border: 1px solid #DDD;
    background: #FFF; 
}

</style>