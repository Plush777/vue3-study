<template>
    <div class="black-bg" v-if="isOpen && true">
        <div class="white-bg">
            <img :src="onerooms[clickIndex].image" alt=""/>
            <h4>{{ onerooms[clickIndex].title }}</h4>
            <p>{{ onerooms[clickIndex].content }}</p>
            <input type="text" v-model.trim="month"/>
            <p>{{ month }} 개월 선택함 : {{ onerooms[clickIndex].price * month }}</p>
            <button @click="callHandleModal(false)" type="button">닫기</button>
        </div>
    </div>
</template>

<script>
/* eslint-disable */

export default {
    name: 'Modal',
    emits: ['handle-modal'],
    data(){
        return {
            month: 1,
        }
    },

    watch: {
        month(next,prev){
            if(isNaN(next) === true){
                alert('한글은 입력할 수 없습니다.');
                this.month = 1;
            }
        }
    },

    props: {
        onerooms: Array,
        clickIndex: Number,
        isOpen: Boolean
    },

    methods: {
        callHandleModal(state){
            this.$emit('handle-modal',state);
        }
    },

    beforeUpdate() {
        if(this.month > 12){
            alert('12개월 이상 입력할 수 없습니다.');
        }
    }
}
</script>