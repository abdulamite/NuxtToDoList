<template>
    <div>
        <div id="list-container">
            <img src="~/assets/clipboard.png" alt="">
            <h1>TO DO LIST</h1>
            <input type="text" placeholder="What needs to get done?" v-on:keyup.enter="addItem" v-model="item">
            <button class="remove_all" v-on:click="clear_items">REMOVE ALL</button>
            <ol>
                <li v-for="thing in item_list" :class="{completed: thing.isDone}">
                    <input type="checkbox" :id=thing.id v-model="thing.isDone" :value=thing.isDone />
                    <span>{{ thing.whatToDo }}</span>
                    <button v-on:click=remove_item(thing)></button>
                 </li>
            </ol>
        </div>
    </div>
</template>

<script>
import ListItem from '~/components/ListItem.vue'

var STORAGE_KEY = 'todos-vuejs-2.0'
// code sourced from https://vuejs.org/v2/examples/todomvc.html originally written by Even You
var itemListStorage = {
  fetch: function () {
    var todos = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
    todos.forEach(function (todo, index) {
      todo.id = index
    })
    itemListStorage.uid = todos.length
    return todos
  },
  save: function (todos) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todos));
  }
}

export default {
    components:{
        ListItem
    },
    data(){
        return{
            item: '',
            item_list: itemListStorage.fetch()
        }
    },
    watch: {
        item_list: {
        handler: function (todos) {
            itemListStorage.save(todos)
        },
        deep: true
        }
    },
    methods:{
        addItem:function(){
            const value = this.item && this.item.trim()
            if (!value) {
                return
            }
            if(this.item){
                this.item_list.push({
                    id: '_' + Math.random().toString(36).substr(2, 9),
                    isDone:false,
                    whatToDo:value
                });
                this.item = '';
            }else{
                console.log('You must enter a valid item');
            }
        },
        complete_item:function(task){
            console.log('Hello World');
        },
        clear_items:function(){
            this.item = ''
            this.item_list = [];
        },
        remove_item:function(task){
            this.item_list.splice(this.item_list.indexOf(task), 1);
        }
    },

    
}
</script>

<style scoped>

#list-container{
    padding:2rem;
}

#list-container>h1{
    padding:.5rem;
}

#list-container>input{
    width:85%;
    border:none;
    height: 4rem;
    padding-left:2rem;
    border-radius: 3px;
    box-shadow: 1px 10px 12px -6px rgba(0, 0, 0, 0.12);
}

#list-container>.remove_all{
    margin:1rem;
    width: 70%;
    background-color:#F77B7B;
    border: none;
    padding:1rem;
    font-weight: bold;
    font-size:1.1rem;
    border-radius: 4px;
    color:#FAFAFA;
}


#list-container>img{
    height: 100px;
    width:auto;
}

#list-container>ol{
    list-style: none;
    margin:auto;
    width: 80%;
    padding:0px;
}

#list-container>ol>li{
    background-color: white;
    border-radius:3px;
    height: 4rem;
    margin: 1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
}

#list-container>ol>li>button{
    border: none;
    height: 20px;
    width: 20px;
    background-color: #f77b7b;
    color: white;
    font-weight: bold;
    border-radius: 25px;
}

#list-container>ol>li>span{
    width: 100%;
    text-align: left;
    padding-left: 1rem;
    font-weight: bold;
}

#checklabel{
    transition:all .2s ease-in-out;
    height: 100%;
    width: 40px;
    border: 2px solid #21B26A;
    display: block;
    border-radius: 20%;
    font-size: 1.2rem;
}


input[type="checkbox"]:checked + label{
  background-color:#21B26A;
  border:#359364;
  animation-name: example;
  animation-duration: .2s;
}

input[type="checkbox"]:checked:after+ label:after{
  background-color:#21B26A;
  border:#359364;
  animation-name: example;
  animation-duration: .2s;
}

li.completed {
    text-decoration: line-through;
    color: grey;
}

@keyframes example {
  from {  transform:scale(1.3);}
  to {  transform:scale(1);}
}



</style>