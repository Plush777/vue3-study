<template>
    <div class="box" v-for="(item,index) in onerooms" :key="item.id">
        <img :src="onerooms[index].image" alt="" width="1024" height="512"/>
        <h4 @click="callHandleModal(true), callUserClick(index)">{{ onerooms[index].title }}</h4> 
        <p>{{ onerooms[index].content }}</p>
        <p>{{ onerooms[index].price }} 원</p>
        <button @click="callCountAdd(index)" type="button">허위매물 신고</button>
        <span>신고수 : {{ counts[index] }}</span>
    </div>
</template>
<script>
/* eslint-disable */
export default {
    name: 'Box',
    emits: ['count-add','handle-modal','user-click'],

    props: {
        onerooms: Array,
        counts: Array,
    },

    methods: {
        callHandleModal(state){
            this.$emit('handle-modal',state);
        },
        callUserClick(index){
            this.$emit('user-click',index);
        },
        callCountAdd(index){
            this.$emit('count-add',index);
        }
    }
}
</script>