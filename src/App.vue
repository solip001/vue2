<template>
	<main class="app">
		<section class="greeting" >
      <h1>
        What's up
        <input type="text" 
          placeholder="name here"
          v-model.trim.lazy="name">
      </h1>
    </section>

		<section class="create_todo">
      <h2>CREATE A TODO</h2>

      <form id="new-todo-form" @:submit.prevent="addTodo">
        <h4>What's on your todo list?</h4>
        <input  
          class="todo_input"
          placeholder="할 일을 입력해 주세요"  
          v-model.trim.lazy="input_content"
        >
        입력 내용 -{{ input_content }}

        <div class="options">          
          <label class="label">
            <input type="radio"     
              name="category" 
              id="category1"
              value="business"
              v-model="input_category">
              <span class="bubble business"></span>
            <div>Business</div>
          </label>
          <label class="label">
            <input type="radio" 
              name="category"
              id="category2"
              value="personal"
              v-model="input_category">
              <span class="bubble personal"></span>
            <div>Personal</div>            
          </label>
          선택한 카테고리 - {{ input_category }}
        </div>
        <input type="submit" value="Add Todo">
      </form>
    </section>

		<section class="todo_list">
      <h3>todo list</h3>
			todos - {{todos}}
      <div class="list">
        <div :class="`todo_item ${todo.done && 'done'}`" v-for="todo in todos" :key="'todo.createAt'">
          <label for="">
            <input type="checkbox" v-model = "todo.done">
            <span class="bubble personal"></span>
          </label>
          <div class="todo_content">
            {{todo.content}}
          </div>
          <div class="actions">
            <button class="delete" v-on:click="removeTodo(todo)">delete</button>
          </div>
        </div>
        <div class="todo_item">
          <label for="">
            <input type="checkbox">
            <span class="bubble bisiness"></span>
          </label>
          <div class="todo_content">
            할 일 2번
          </div>
        </div>
      </div>
		</section>

	</main>
</template>

<script setup>
	import { computed } from '@vue/reactivity';
import { ref, watch, onMounted } from 'vue';

  const name= ref('');
  const input_content= ref(null);
  const input_category= ref(null);
  const todos = ref([])

  // 시간순으로 정리(최신이 위에 오게)
  const todos_asc = computed(()=>{todos.value.sort((a,b)=>b.createAt-a.createAt)})

  //삭제 함수
  const removeTodo = (item)=> {
    todos.value = todos.value.filter((aa)=>aa !== item)
  }

 //할일 입력값들을 받아오는 함수
const addTodo = () => {
	console.log('할일 입력값을 받아오는 함수 실행')

  //입력 값이 없거나 카테고리 미선택 씨 코드블록 밖으로 빠져나감
  if(input_content.value === "" || input_category === null){
    return
  }
  todos.value.push({
    content:input_content.value,
    category:input_category.value,
    done:false,
    creatAt: new Date().getTime() // 시간 순으로 순서를 널기 위해 UTC1970년 1월 1일 부터 현재가지 몇 초 지났는 지 알아오는 것.
  })
	}

//todos가 바귀는 것 감지
watch(todos,(newVal)=>{
  console.log('투두스 감지', newVal)
  localStorage.setItem('todos',newVal)
  localStorage.setItem('todos',JSON.stringify)
},{deep:true})
// deep - 속성의 프로퍼티나 하위 랩스도 감지

//이름 입력하는 것을 감지하고 로컬스토리지에 저장, 업데이트
watch(name,(newVal)=>{
    localStorage.setItem('name',newVal)
  })

	//새로 열었을때 로컬스토리지에서 불러옴 (없을때는 비워놓음)
	onMounted(()=>{
    name.value = localStorage.getItem('name') || '';
    // todos.value = localStorage.getItem('todos') || '';
  })
</script>
<style  lang="scss" scoped>
$primary: #ea40a4;
$light: #eee;
$grey: #888;
$dark: #313154;
$business: #3a82ee;
$personal: $primary;
$danger: red;


$shadow: 0 1px 3px rgba(0,0,0,0.2);

$business-glow: 0 0 6px rgba(58, 130, 238, 0.5);
$personal-glow: 0 0 6px rgba(234, 64, 164, 0.5);

@mixin center {
  display: flex;
  align-items: center;
  justify-content: center;
}

* { margin: 0; padding: 0; box-sizing: border-box; }

input:not([type="radio"]) {
  appearance: none;
  border: none;
  outline: none;
  background: none;
  cursor:initial;
}

body {
  background:$light;
  color:$dark;
}

section {
  margin:2rem 0;
  padding:0 1.5rem;
}

h2 {
  color: $primary;
  font-size: 1rem;
}
h3 {
  color: $dark;
  font-size: 1rem;
  margin-bottom: 0.5rem;
}
h4 {
  color: $grey;
  font-size: 0.85rem;
  margin-bottom: 0.5rem;
}

.greeting {
  .title{

    input{
      margin-left: 0.5rem;
      font-size: large;
      font-weight: 700;

      &::placeholder{
        font-size:0.8rem;
        font-weight: 400;
      }
    }
  }
}

.create_todo {
  .todo_input {
    width: 100%;
    background: #fff;
    padding: 1rem 1.5rem;
    font-size: 1.1rem;
    color: $dark;
    border-radius: 0.5rem;
    box-shadow:$shadow;
    margin-bottom: 1.5rem;
  }

  .options {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 1rem;
    margin-bottom: 1.5rem;    
  }

  input[type="submit"] {
    @extend .todo_input;

    color:#fff;
    background: $primary;
    box-shadow:$personal-glow;
    cursor: pointer;
    transition: 0.2s ease-in;

    &:hover {
      transform: translate(0.2rem, 0.2rem);
    }
  }
}



  
.label{ 
  @include center;
  flex-direction: column;      
  padding:1.5rem;
  background: #fff;
  border-radius: 0.5rem;
  box-shadow: $shadow;

  input {
    display: none;

    &:checked ~ .bubble::after {
      width:10px; height: 10px;
      opacity:1;
    }
  }

  .bubble {
    @include center;

    width: 20px; height: 20px;
    border-radius: 50%;
    border: 2px solid $business;
    box-shadow:$business-glow;

    &::after {
      display: block;
      content: "";
      width:0; height: 0;
      background: $business;
      border-radius: 50%;
      box-shadow: $business-glow;
      opacity:0;
      transition: 0.3s ease-in;
    }

    &.personal {
      border: 2px solid $personal;
      box-shadow:$personal-glow;

      &::after{
        background:$personal;
        box-shadow: $personal-glow
      }

    }
  }

  div {
    color: $dark;
    font-size: 1.1rem;
    margin-top: 1rem;
  }

  
}
.todo_list .list {
	margin: 1rem 0;

  .todo_item {
    display: flex;
    align-items: center;
    background-color: #FFF;
    padding: 1rem;
    border-radius: 0.5rem;
    box-shadow: var(--shadow);
    margin-bottom: 1rem;

    label {
      @extend .label;
      padding:0;
      display: block;
      margin-right: 1rem;
      cursor: pointer;
    }
    .todo_content {
      flex: 1;

      input {
        color: var(--dark);
        font-size: 1.125rem;
        width: 95%;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
      }
    }
    .actions {
      display: flex;
      align-items: center;

      button {
        display: block;
        padding: 0.5rem;
        border:none;
        border-radius: 0.25rem;
        color: #FFF;
        cursor: pointer;
        transition: 0.2s ease-in-out;

        &:hover {
          transform: translate(0.05rem, 0.05rem);
        }
        .edit {
          margin-right: 0.5rem;
          background-color: $primary;
        }
        &.delete {
          background-color: $danger;
        }
      }
    }  
    &.done .todo_content input {
      text-decoration: line-through;
      color: $grey;
    }  
  } 
}
</style>