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
    }
    
    const stopEvent = (e) => {
      e.stopPropagation();
    }
  
// モーダル機能




</script>

<template>
  <AppHeader color1="green" >ToDoリスト</AppHeader><br>
<main>
  <input type="text" size="30" v-model="newTodo">
  <button @click="addTodo()">追加</button>

  <TodoList :todos="todos" @removeTodo="removeTodo"/>




<!-- {/* モーダル機能 */} -->


<button v-on:click="openModal">利用規約</button>

<div id="overlay" v-show="showContent" @click="closeModal">
  <div id="content" @click="stopEvent">
    <h1>利用規約</h1>
      <p>
        この利用規約（以下，「本規約」といいます。）は，＿＿＿＿＿（以下，「当社」といいます。）がこのウェブサイト上で提供するサービス（以下，「本サービス」といいます。）の利用条件を定めるものです。登録ユーザーの皆さま（以下，「ユーザー」といいます。）には，本規約に従って，本サービスをご利用いただきます。
      </p>
      <h2>第1条（適用）</h2>
      <ol>
        <li>
          本規約は，ユーザーと当社との間の本サービスの利用に関わる一切の関係に適用されるものとします。
        </li>
        <li>
          当社は本サービスに関し，本規約のほか，ご利用にあたってのルール等，各種の定め（以下，「個別規定」といいます。）をすることがあります。これら個別規定はその名称のいかんに関わらず，本規約の一部を構成するものとします。
        </li>
        <li>
          本規約の規定が前条の個別規定の規定と矛盾する場合には，個別規定において特段の定めなき限り，個別規定の規定が優先されるものとします。
        </li>
      </ol>
    <button v-on:click="closeModal">閉じる</button>
  </div>
</div>
<!-- {/* モーダル機能 */} -->
</main>

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