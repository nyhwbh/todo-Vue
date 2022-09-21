<template>
  <div>
    <ul>
      <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem" class="shadow" >
        <i class="checkBtn fa-solid fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" v-on:click="toggleComplete(todoItem,index)"></i>
        <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
        <span class="removeBtn" v-on:click="removeTodo(todoItem,index)">
          <i class="fa-solid fa-trash-can"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data: function() {
    return{
      todoItems: []
    }
  },
  methods :{
    removeTodo:function(todoItem,index) {
      console.log(todoItem, index);
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    },
    toggleComplete:function(todoItem,index){
      console.log('hi'+index)
      todoItem.completed = !todoItem.completed;
      // localstorage에 대이터 갱신
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item,JSON.stringify(todoItem));
    }
  },
  created: function(){
    if(localStorage.length > 0){
      for(var i=0; i<localStorage.length; i++){
        if(localStorage.key(i) !== ''){
          JSON.parse(localStorage.getItem(localStorage.key(i)));
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
      }
    }
  }
}
</script>

<style scoped>
ul{
  list-style-type: none;
  padding-left: 8px;
  margin-top: 0;
  text-align: left;
}

li{
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin:0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.removeBtn {
  margin-left:auto;
  color:#de4343
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right:5px;
  margin-top: 18px;
}
.checkBtnCompleted {
  color: #b3adad
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
</style>