<template>
    <div class="new-task">
        <input type="text" class="form-element" 
               placeholder="digite a tarefa..."
               @keydown.enter="add" 
               v-model="name"      
        >
        <button class="form-element" @click="add">+</button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name : ''
        }
    },
    methods : {
        add() {
            if (this.name!='') {
                this.$emit('taskAdded', {name : this.name})
                this.name = ''
            }
        }
    }
}
</script>

<style scoped>
    .new-task {
        margin : 75px
    }

    .form-element {
        outline : none;
        font-size: 1rem;
        border : 1px solid #FFF;
        padding: 5px 10px 8px;
        color: white;
    }

    input.form-element {
        width : 500px;
        background-color : navy;
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
    }

    button.form-element {
        cursor : pointer;
        border-left : none;
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
        background-color : blue;
    }
</style>