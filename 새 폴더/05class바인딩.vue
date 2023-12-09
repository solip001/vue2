<template>
  <div>
    <h3>class바인딩</h3>
    <p class="text" v-bind:class="ClassObj[1]">텍스트입니다</p>
    <p class="text" v-bind:class="ClassObj[0],ClassObj[1]">텍스트입니다</p>
    <hr>
    <p class="text" v-bind:class="ClassObj2">텍스트입니다</p>
    <button v-on:click="isActive = !isActive">togle active</button>
    <button v-on:click="hasWanning = !hasWanning">togle danger</button><!-- 이 버튼은 왜 작동이 안될가...-->
    <br>
    <button @:click="toggle">togle 전체</button> <!-- v-on = @로 축약 가능-->
  </div>
</template>

<script>
import { reactive,ref } from 'vue';

export default {
  setup () {
    const ClassObj = ['active', 'danger']
    // const ClassObj = 'active danger' 이렇게 작성도 가능
    
    const isActive = ref(false);
    const hasWanning = ref(false);
    function toggle(){
      isActive.value = !isActive.value;
      hasWanning.value = !hasWanning.value
    }

    const ClassObj2 = reactive({
      active:isActive,
      danger:hasWanning
    })


    return {ClassObj,isActive,ClassObj2,toggle}
  }
}
</script>

<style lang="scss" scoped>
  .text{
    font-size: 22px;
    font-weight: 800;
  }
  .danger{
    background: red;
    color: yellow;
  }
  .active{
    background: green;
  }
</style>