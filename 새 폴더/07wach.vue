<template>
  <div>
    <div class="box">
      <h2>watch</h2>
      <p class="description">
        reactivity 데이터의 상태가 변경을 감지하여 다른 작업을 수행
      </p>
      <p>wach(감지할 반응형 데이터 함수)</p>
      <p>watch(감지할 reactive 데이터(새로운 데이터, 기존데이터) => {실행구}) </p>
      <br>
      <p>
        watch(함수의 return 값 데이터,(새로운 데이터, 기존데이터) => {실행구}) 
      </p>
      <p>
        watch([데이터1, 데이터2]([새로운 데이터1, 새로운 데이터2],[기존데이터21, 기존데이터2]) => {실행구}) 
      </p>
    </div>
  </div>
</template>

<script>
import {reactive, ref, watch} from 'vue'
export default {
  setup () {
    const message = ref('안녕하세요')

    watch(message,(newValue,oldValue)=>{
      
    })

    const x = ref(0)
    const y = ref(0)

    //x,y의 합계값을 감지
    watch(()=> x.value + y.value,(sum, oldSum)=>{      
      console.log('새로운 합계값',sum)
      console.log('dlwjs 합계값',oldSum)
    })

    //여러개를 동시에 감지 할수 있음
    watch([x,y],([newX,newY],[oldX,oldY])=>{
      console.log('새로운x:',newX,'기존X',oldX)
      console.log('새로운Y:',newY,'기존Y',oldY)

    })

    // reactivity 객체도 감지 -> 함수안에 넣어서
    const hotel = reactive({
      name: 'shilla',
      emptyRoom:40
    })
    watch(()=>hotel.emptyRoom,(new값, old값)=>{
      console.log('새로운 방 갯수-', new값)
      console.log('이전 방 갯수-', old값)
    })


    return {message}
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