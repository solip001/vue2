<template>
  <div>
    <h1>computed - 계산된 속성, 함수</h1>
    <p>-템플릿 문법이 길어지면 가독성이 떨어지고 유지보수가 어려워짐을 방지</p>
    <p>-계산한 것을 캐싱(보관)해주고, 화면이 업데이트 될때 캐싱을 호출함. 데이터가 변경될때 다시 계산</p>
  </div>
  <div class="box">
    <h2>점심식당</h2>
    <p>점심메뉴가 나왔나요?</p>
    <!-- 일반함수 - computed 차이
    1. 아래처럼 여러번 사용 할떄 일반 함수는 사용 갯수만큼 호출 하는 반면 coputed는 단 한번만 불러옴(콘솔창 확인)
    2. 버튼 클릭틍의 이벤트식 일반 한수는 반복해서 호출을 함. 
    -->
    <p>일반함수 - {{ exitMenu() }}</p>
    <p>일반함수 - {{ exitMenu() }}</p>
    <p>일반함수 - {{ exitMenu() }}</p>
    <p>computed - {{ hasMenu }}</p>
    <p>computed - {{ hasMenu }}</p>
    <p>computed - {{ hasMenu }}</p>
    <button v-on:click = "counter++">{{ counter }}</button>
  </div>
</template>

<script>
import { computed,ref } from '@vue/reactivity'

export default {
  setup () {
    const lunch = {
      name : '점심식단',
      menu:[
        '마라탕',
        '샌드위치',
        '햄버거'
      ]
    }
    
    // 자바스크립트식 함수 표현
    function exitMenu(){
      console.log('일반함수')
      return  lunch.menu.length > 0 ? '네 준비되어있습니다' : '아직 준비되지 않았습니다.'
    }

    // 뷰 식 함수 표현
    const hasMenu = computed(
      () => {
        console.log('computed')
        return  lunch.menu.length > 0 ? '네 준비되어있습니다' : '아직 준비되지 않았습니다.'
      }
    )
    
      //counter
      const counter = ref(0);


    return {lunch,exitMenu,hasMenu,counter}
  }
}
</script>

<style lang="scss" scoped>

</style>