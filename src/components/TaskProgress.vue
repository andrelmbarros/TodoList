<template>
    <div class="tasks-progress">
        <span class="progress-value">{{progress}}%</span>
        <div class="progress-bar" :style="{width : progress + '%'}"></div>
    </div>
</template>

<script>
export default {
    props : {
        progress: {type : Number, default : 0}
    }
}
</script>

<style scoped>
    .tasks-progress {
        position : relative;
        width : 80%;
        border : 1px solid gray;
        color : black;
        border-radius: 8px;
        margin-left: 150px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .progress-bar {
        position : absolute;
        border-radius: 8px;
        height: 100%;
        background-color: green;
        align-self: flex-start;
    }

    .progress-value {
        z-index: 1;
        font-size : 1.5rem
    }
</style>