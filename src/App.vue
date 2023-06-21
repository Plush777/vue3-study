<template>
  <div class="menu">
    <a v-for="(item,index) in menus" :key="index">{{ item }}</a>
  </div>

  <Transition name="fade">
    <Modal :onerooms="onerooms" :isOpen="isOpen" :clickIndex="clickIndex" @handle-modal="handleModal"/>
  </Transition>

  <div class="boxWrap">
    <Discount v-if="isShow"/>
    <button type="button" @click="priceSort">가격순정렬</button>
    <button type="button" @click="sortReset">되돌리기</button>
    <Box :onerooms="onerooms" :counts="counts" @count-add="countAdd" 
    @user-click="userClick" @handle-modal="handleModal"/>
  </div>  
</template> 

<script>  
import data from './data/data.js';
import Discount from '@/components/Discount';
import Modal from '@/components/Modal';
import Box from '@/components/Box';

export default {
  name: 'App',

  data(){
    return{
      clickIndex: 0,
      prices: [60,70,80],
      menus: ['Home','Shop','About'],
      products: ['역삼동원룸','천호동원룸','마포구원룸'],
      oneroomsCopy: [...data],
      onerooms: data,
      counts: Array(data.length).fill(0), //배열에 data 개수만큼 0으로 채운다.
      isOpen: false,
      isShow: true
    }
  },

  methods: {
    countAdd(index){
      this.counts[index]++;
    },
    userClick(index){
      this.clickIndex = index;
    },
    handleModal(state){
      this.isOpen = state;
    },
    priceSort(){
      this.onerooms.sort(function(a,b){
        return a.price - b.price;
      })
    },
    sortReset(){
      this.onerooms = [...this.oneroomsCopy];
    }
  },  

  // mounted(){
  //   setTimeout(() => {
  //     this.isShow = false;
  //   }, 2000);
  // },

  components: {
    Discount: Discount,
    Modal: Modal,
    Box: Box
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 1024px;
  margin: 0 auto;
}

.menu{
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  z-index: 0;
  max-width: 1024px;
  width: 100%;
  margin-top: 30px;
  margin-bottom: 30px;
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}

.menu a{
  color: white;
  padding: 10px;
}

.box +.box{
  margin-top: 30px;
}

body{
  margin: 0;
}

div{
  box-sizing: border-box;
}

.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, .5);
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  padding: 20px;
  z-index: 1;
}

.white-bg{
  width: 100%;
  background: white;
  border-radius: 8px;
  padding: 20px;
}

.boxWrap{
  padding-top: 120px;
}

.discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

.fade-enter-from{
  opacity: 0;
}

.fade-enter-active{
  transition: .5s;
}

.fade-enter-to{
  opacity: 1;
}


.fade-leave-from{
  opacity: 1;
}

.fade-leave-active{
  transition: .5s;
}

.fade-leave-to{
  opacity: 0;
}
</style>
