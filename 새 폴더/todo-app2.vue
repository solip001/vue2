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
          v-model="input_content"
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
			todo_list
		</section>

	</main>
</template>

<script setup>
	import { ref, watch, onMounted } from 'vue';

  const name= ref('');
  const input_content= ref(null);
  const input_category= ref(null);
  const todos = ref([])

 //할일 입력값들을 받아오는 함수
const addTodo = () => {
	console.log('할일 입력값을 받아오는 함수 실행')

    todos.value.push({
      content:input_content.value,
      category:input_category.value
    })
	}


//이름 입력하는 것을 감지하고 로컬스토리지에 저장, 업데이트
watch(name,(newVal)=>{
    localStorage.setItem('name',newVal)
  })

	//새로 열었을때 로컬스토리지에서 불러옴 (없을때는 비워놓음)
	onMounted(()=>{
    name.value = localStorage.getItem('name') || '';
  })
</script>
