# props 나머지 내용 조금 & 저번시간 숙제

props에 대한 자잘한 추가내용을 배워봅시다.

별건 아니고 props로 데이터를 전송할 때 굳이 밑에 있는 데이터가 아니라도

문자, 숫자, array object 자료도 직접 집어넣을 수 있습니다. 

<br/>

## props 보내는 여러가지 방법

```html
<Discount :데이터이름="[1,2,3]" />
<Discount :데이터이름="{ age:20 }" />
<Discount :데이터이름="100" />
<Discount 데이터이름="안녕하쇼" />
```

각각 array, object, 숫자, 문자보내기입니다.

콜론을 안붙이면 문자로 전달됩니다.

<br/>

`오브젝트 : {name : 'kim', age : 20}` 이라는 object 자료가 밑에 있는데

이걸 name, age 각각 props로 보내고 싶으면 

```html
<Discount :데이터이름="오브젝트.name" :데이터이름="오브젝트.age"  />
```

이런 식으로 적어야하는데 이게 너무 번거로우면

```html
<Discount v-bind="오브젝트명" />
```

이런 식의 특별한 문법을 사용해도 다 보내집니다.

근데 이러지말고 애초에 그냥 object 자료 통째로 보내면 되지않습니까. 

<br/>

## 저번시간 숙제 : 상품목록을 `<Card>` 컴포넌트화하기

① 저는 Card.vue 부터 만들었습니다.

```html
(Card.vue)

<template>
  <div>
    <img :src="a.image" class="room-img">
    <h4> {{a.title}} </h4>
    <p>{{a.price}} 원</p>
   </div>
</template>

(밑엔 생략)
```
v-for까지 넣어서 상품 6개를 전부 <Card>로 만들 수도 있겠지만

저는 상품 한개만 <Card>로 축약하고 싶어서 이렇게 작성했습니다.

님들은 아무렇게나 하십시오 그냥 취향입니다.  

그리고 모달창 여는 기능은 나중에 할거라 잠깐 지웠습니다.

<br/>

그리고 App.vue에서 import하고 등록하고 사용했습니다.

```html
<Card/>
```

```js
import Card from './Card.vue'

export default {
  components : { 
    Card
  }
}
```

하지만 아무것도 안나오는 이유는 당연히 

Card.vue 안에 a.title 이런게 있던데 a라는 변수엔 아무것도 없기 때문입니다.

a가 뭐였죠? 반복문 돌릴 때 나오는 그 하나하나의 상품데이터자료 아니었습니까.

그걸 props로 전송해주면 이제 제대로 상품명, 상품가격 이런게 나오겠군요.

<br/>

② a에 필요한 정보를 props로 보내줍니다.

이전시간에 a는 반복문돌릴 때 나온 하나하나의 상품데이터라고 했습니다.

원룸들 : [ {}, {}, {}, {}, {}, {} ] 이거 안에 있던 하나의 {} 데이터요.

이걸 그대로 똑같이 props로 보내주면 되겠군요.

```html
(App.vue)
<Card :원룸="원룸들[0]" />
```
저는 이쁘게 원룸이라고 작성해서 {} 이거 하나를 보내봤습니다. 첫째상품 데이터겠네요. 

그리고 props를 보냈으면 등록하고 위에서 쓰셔야합니다. 

```html
(Card.vue)

<template>
  <div>
    <img :src="원룸.image" class="room-img">
    <h4> {{원룸.title}} </h4>
    <p>{{원룸.price}} 원</p>
   </div>
</template>


<script>
export default {
  props : {
    원룸 : Object
  }
}
</script>
```

원룸이라는 이름으로 props를 보냈으니까

데이터바인딩할 때도 `{{a}}` 대신 `{{원룸}}` 어쩌구 해주면 되겠군요. 

이러면 `<Card>`가 첫째 상품으로 잘 이쁘게 보입니다. 끝 

그럼 나머지 5개의 상품도 알아서 만들어보십시오. 

`<Card>` 여기에 반복문 돌려도 됩니다. 반복문도 연습삼아 써보십시오