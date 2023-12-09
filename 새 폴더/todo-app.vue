<template>
	<main class="app">
		<section class="greeting">
			<h1 class="title">
				What's Up! 
				<input type="text" placeholder="이름 입력" v-model.trim.lazy="name">
				{{ name }}
			</h1>
		</section>
		<section class="create_todo">
			create_todo
		</section>
		<section class="todo_list">
			todo_list
		</section>

	</main>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue';

	const name = ref('');


	//이름 입력을 인지하고 로컬 스토리지에 저장
	watch(name,(newName)=>{
		localStorage.setItem('name', newName)
    })

	//새로 열었을때 로컬스토리지에서 불러옴 (없을때는 비워놓음)
	onMounted(()=>{
    name.value = localStorage.getItem('name') || '';
  })
</script>
