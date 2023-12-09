<template>
  <div class="box">
    <h2 v-if="visible" style="color: red;">hello vue3</h2>
    <h2 v-else  style="color: green;">hello vue3</h2>
    <button @:click="visible=!visible">Toggle</button>
  </div>
  <div class="box">
    <button @:click = "type='A'">A</button>
    <button @:click = "type='B'">B</button>
    <button @:click = "type='C'">C</button>
    <button @:click = "type='D'">D</button>
    <h2 v-if="type === 'A'">A 버튼을 클릭했습니다</h2>
    <h2 v-else-if="type === 'B'">B 버튼을 클릭했습니다</h2>
    <h2 v-else-if="type === 'C'">C 버튼을 클릭했습니다</h2>
    <h2 v-else>A, B, C가 아닙니다</h2>
  </div>
  <div class="box">
    <div v-if="visible2">
      <h1>Title</h1>
      <p>paragraph1 - 하나의 조건으로 여러개의 태그 (dom 요소)를 렌더링 해준다</p>
      <p>paragraph2</p>
    </div>
    <button @:click="visible2 = !visible2">Toggle</button>
    <hr>
    <h2 v-show="disShow">Title입니다</h2>
    <p>v-show 는 code 상에선 존재. style - display 속성을 변경한다</p>
    <p>v-if는 html 코드 자체가 사라진다</p>
    <button @:click="disShow = !disShow">Show Toggle</button>
  </div>
</template>

<script>
import {ref} from 'vue'

export default {
  setup () {
    const visible = ref(false)
    const type = ref('A')
    const visible2 = ref(true)

    // v-show
    const disShow = ref(true)

    return { visible,type,visible2,disShow }
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
  hr{
    margin: 2rem 0;
  }
  button{
    padding: 4px 10px;
    border: 2px solid navy;
    border-radius: 5px;
    background: #fff;
    color: navy;
  }
  p + button, div + button{
    margin-top: 10px;
  }
</style>