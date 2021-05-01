<template>
    <div class="task" :class="stateClass" @click="$emit('taskStateChanged', task)"> 
        <span class="close" @click.stop="$emit('taskDeleted', task)">
            x
        </span>
        {{task.name}}
    </div>
</template>

<script>
export default {
    props : {
        task : {type : Object, required : true}
    },
    computed : {
        stateClass() {
            return {
                pending : this.task.status==1,
                started : this.task.status==2,
                done : this.task.status==3
            }
        }
    }
}
</script>

<style scoped>
    .task {
        position : relative;
        box-sizing : border-box;
        width : 150px;
        height: 75px;
        padding : 10px;
        border-radius: 8px;
        font-size: 1rem;
        font-weight: 300;
        cursor : pointer;
        user-select: none;
        display : flex;
        margin : 10px;
        align-items: center;
    }

    .pending {
        color: white;
        border-left : 12px solid rgb(150, 54, 54);
        background-color: red
    }

    .started {
        color: black;
        border-left : 12px solid rgb(177, 177, 35);
        background-color: yellow;
    }

    .done {
        color: white;
        border-left: 12px solid rgb(28, 80, 28);
        background-color: green;
        text-decoration: line-through;
    }

    .pending .close{
        background-color :  rgb(150, 54, 54);
    }

    .started .close{
        background-color : rgb(177, 177, 35)
    }

    .done .close {
        background-color:  rgb(28, 80, 28);
    }

    .close {
        position : absolute;
        top: 10px;
        right: 10px;
        font-size: 0.5rem;
        height: 10px;
        width: 10px;
        border-radius: 5px;
    }
</style>