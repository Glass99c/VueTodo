<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem"
        @keyup.enter="addTodo">
        <span @click = "addTodo" class="addContainer">
            <i class="fa-solid fa-plus addBtn"></i>
        </span>
        <AlertModal v-if="showModal" @close="showModal = false">
            <h3 slot="header">
                경고!
                <i class="closeModalBtn fa-solid fa-xmark" @click="showModal=false"></i>
            </h3>
            <h3 slot="body">
                으잉
            </h3>
        </AlertModal>
    </div>
</template>

<script>
import AlertModal from './common/AlertModal.vue'
export default {
    data : function(){
        return{
            newTodoItem: "",
            showModal: false
        }
    },
    methods : {
        addTodo(){
            if(this.newTodoItem!==''){
                this.$emit('addTodoItem', this.newTodoItem);
                this.clearInput();
            }else{
                this.showModal = !this.showModal;
            }
        },
        clearInput(){
            this.newTodoItem='';
        }
    },
    components:{
        'AlertModal': AlertModal
    },
}
</script>

<style scoped>
    input:focus{
        outline: none;
    }
    .inputBox {
        background : white;
        height : 50px;
        line-height : 50px;
        border-radius : 5px;
    }
    .inputBox input {
        border-style : none;
        font-size : 0.9rem;
    }
    .addContainer {
        float : right;
        background : linear-gradient(to right, #6478FB, #8763FB);
        display : block;
        width : 3rem;
        border-radius : 0 5px 5px 0;
    }
    .addBtn {
        color: white;
        vertical-align: middle;
    }
    .closeModalBtn{
        color: #42b983;
    }
</style>