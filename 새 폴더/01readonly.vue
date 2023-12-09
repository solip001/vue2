<template>
  <div>
    <p>{{ book }}</p>
    <p>저자 : {{ book.author }}</p>
    <p>제목 : {{ title }}</p>
    <p>가격 : {{ prize }}</p>
    <p>소개 : {{ description }}</p>
  </div>
</template>

<script>
import { reactive, readonly, toRefs } from 'vue'
export default {
  setup () {
    const book = reactive({
      author : 'vue team',
      year : 2023,
      title : 'vue 3 guide',
      description : '초보자를 위한 뷰의 모든 것',
      prize : 'Free'
    })
    const {title, prize, description} = toRefs(book);

    book.author = '그린컴퓨터 개발팀'
    
    const priceSpecial = readonly(prize); // 이후에 수정 되지 않도록 고정.. 인데 작동 안함

    title.value = 'Vue 박살!'
    prize.value = 10000;

    return {book, title, prize, description, priceSpecial}
  }
}
</script>

<style lang="scss" scoped>

</style>