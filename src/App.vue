<script setup>
import AppHeader from './components/AppHeader.vue'
import TodoList from './components/TodoList.vue'
import { ref } from 'vue'

const todos = ref([])
const newTodo = ref('')

const addTodo = () => {
  todos.value.push(newTodo.value)
  newTodo.value = ''
  }

const removeTodo = (index) => {
  todos.value.splice(index, 1)
}  


// モーダル機能
const showContent = ref(false);

    const openModal = () => {
      console.log('click');
      showContent.value = true;
    };

    const closeModal = () => {
      showContent.value = false;

      const clickEvent = () => {
            context.emit('from-child');
          };
          const stopEvent = (e) => {
            e.stopPropagation();
          }
        }
// モーダル機能




</script>

<template>
  <AppHeader color1="green" >ToDoリスト</AppHeader><br>
<main>
  <input type="text" size="30" v-model="newTodo">
  <button @click="addTodo()">追加</button>

  <TodoList :todos="todos" @removeTodo="removeTodo"/>
</main>



{/* モーダル機能 */}
<button v-on:click="openModal">Click</button>

<div id="overlay" v-show="showContent">
  <div id="content">
    <p>これがモーダルウィンドウです。</p>
    <button v-on:click="closeModal">Close</button>
  </div>
</div>
<div id="overlay" v-on:click="clickEvent">
    <div id="content" v-on:click="stopEvent">
      <p><slot></slot></p>
      <button v-on:click="clickEvent">close</button>
    </div>
</div>
{/* モーダル機能 */}


</template>

<style>
  main{
    background-color: #fdf6e3;
  }

  /* モーダル機能 */
  #overlay {
      /*　要素を重ねた時の順番　*/
      z-index: 1;

      /*　画面全体を覆う設定　*/
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);

      /*　画面の中央に要素を表示させる設定　*/
      display: flex;
      align-items: center;
      justify-content: center;
    }

    #content {
      z-index: 2;
      width: 50%;
      padding: 1em;
      background: #fff;
    }
  /* モーダル機能 */

</style>