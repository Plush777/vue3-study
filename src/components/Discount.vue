<template>
    <div class="discount">
        <h4>지금 결제하면 {{ discountValue }}% 할인!!!</h4>
    </div>
</template>

<script>
/* eslint-disable */
export default {
    name: 'Discount',

    data(){
        return{
            discountValue: 20
        }
    },

    methods: {
        minus(){
            this.discountValue--;
        }
    },

    mounted(){
        let timer = setInterval(() => {
            if(this.discountValue === 0){
                clearInterval(timer);
                return;
            } else {
                this.minus();
            }
        }, 1000);
    }
}
</script>