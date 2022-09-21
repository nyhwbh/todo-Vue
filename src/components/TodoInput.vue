<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="fa-solid fa-plus addBtn"></i>
    </span>
    <Modal v-if="showModal" @close="showModal = false">
        <template v-slot:header>
          <h3>경고!</h3>
          <span @click="showModal = false">
            <i class="closeModalBtn fa-sharp fa-solid fa-xmark"></i>
          </span>
        </template>
        <template v-slot:body> 아무것도 입력하지 않았습니다.</template>
      </Modal>
  </div>
</template>

<script>
import Modal from "./common/MoDal"
export default {
  data: function() {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods:{
    addTodo() {
      if(this.newTodoItem !== ''){
        this.$emit('addTodoItem', this.newTodoItem)
        this.clearInput();
      }else{
        this.showModal = !this.showModal
      }
    },
      clearInput() {
        this.newTodoItem = ''
      }
    },
    components:{
      Modal
    }
  }

</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
  width: 85%;
  height: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478Fb, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color:white;
  vertical-align: middle;
}
.closeModalBtn{
  color: #42b983;
  font-size: 20px;
}
</style>