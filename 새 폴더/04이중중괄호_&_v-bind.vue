<template>
  <div class="box">
    <h3>이중중괄호 (콧수염 괄호)</h3>
    <p>{{ msg }}</p>
    <p v-once>{{ msg }}</p> 
    <button v-on:click = "msg = msg+'@'">click</button>
    <ul class="description">
      <li>이중중괄호는 데이터의 변경이 있을때마다 자동으로업데이트</li>
      <li>v-once = 데이터를 한 번만 불러오는 일회성 코드. 테이터가 변경되어도(데이터 변경 이벤트가 실행되도) 업데이트 되지 않음</li>
    </ul>
  </div>
  <div class="box">
    <h3>text, html</h3>
    {{ rowHtml }}
    <p v-text="rowHtml"></p>
    <p v-html="rowHtml"></p>
    <p v-html="rowHtml2"></p>
    <ul class="description">
      <li>이중중괄호는 데이터를 html이 아닌 일반 텍스트로 인식함</li>
      <li>v-text : 엘리먼트의 텍스트 컨텐츠를 업데이트 / 이중중괄호와 동일</li>
      <li>v-html : 엘리먼트의 html태그를 업데이트</li>
    </ul>
  </div>
  <div class="box">
    <h3>속성(attribute) 바인딩</h3>
    <p title="이게 뭐여">마우스를 올려보세여</p>
    <p v-bind:title="dynamicTitle">마우스를 올려보세여</p>
    <p :title="dynamicTitle">마우스를 올려보세여</p> <!-- 이런식으로 v-bind 생략도 됨-->
    <input type="text" placeholder="텍스트 입력" v-bind:disabled="inputDis">
    <button v-on:click="inputDis =!inputDis">toggleButton</button>
    <br>
    <input type="text" size="30" placeholder="여러개의 속성을 적용">
    <input v-bind="attrs">
    <ul class="description">
      <li>이중중괄호는 html태그위속성으로는 사용 못함. 대신에 v-bine 이용</li>
      <li>boolen(true/false) 속성에서도 v-bind 사용</li>
      <li>여러개의 속성을 한번에 바인딩 가능</li>
      <li>축약형으로 : 만 쓰기도 함 <br>ex)<input :="attrs"></li>
    </ul>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity';
import { reactive } from 'vue';


export default {
  setup () {
    const msg = ref('안녕하세요!')
    const rowHtml = '<strong>얼룩말</strong>'
    const rowHtml2 = '<strong style="color:red;">얼룩말</strong>'
    
    // 속성(attribute) 바인딩
    const dynamicTitle = ref('손을 올려놓았나요?')
    const inputDis = ref(false)
    const attrs = reactive({
      type : "text",
      size : "30",
      placeholder: "여러개의 속성을 적용" 
    })


    return {msg,rowHtml,rowHtml2,dynamicTitle,inputDis,attrs}
  }
}
</script>

<style lang="scss" scoped>
  .box{
    border: 1px solid #dbdbdb;
    margin: 50px 10px;
    padding: 20px;
    .description{
      color: grey;
      font-size: 16px;
      padding-top: 20px;
    }
  }
  .box +.box{
    margin-top: 40px;
  }
</style>