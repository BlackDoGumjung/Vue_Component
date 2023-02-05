<template>
  <li>
    <h2>{{ name }}{{ isFavorite ? '(Favorite)' : '' }}</h2>
    <button @click="toogleFavorite">Toogle Favorite</button>
    <button @click="toggleDetails">
      {{ detailsAreVisible ? 'Hide' : 'Show' }} Details
    </button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul>
    <button @click="$emit('delete', id)"></button>
  </li>
</template>
<!-- 지원되는 프로퍼티 값 -->
<!-- : String, Number, Boolean, Array, Object, Date, Function, Symbol, 생성자 함수도 타입이 될 수 있음 -->
<script>
export default {
  // props: ['name', 'phoneNuber', 'emailAddress', 'isFavorite'],
  //물론 이렇게 써도 되지만 협업 시에는 타입을 기재해주는 게 좋음
  props: {
    // name: String,
    id: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    }, // 프로퍼티를 한줄로만 쓸 수도 있되, 타입과 필수 여부도 정해줄 수 있음 (이 경우는 오브젝트 형태)
    phoneNumber: {
      type: String,
      required: true,
    }, // 만약 필수 프로퍼티를 빼고 컴포넌트를 구성하게 되면 렌더링은 되는데 워닝은 뜨게 됨!
    emailAddress: {
      type: String,
      required: true,
    },
    isFavorite: {
      type: Boolean,
      required: false,
      default: false,
      //필수 아닌 값에 기본 값 설정하기 '즐겨찾기 아님'
      // validator: function (value) {
      //   //참 거짓을 가지는 검증자 함수를 만들 수도 있음, 유효성 로직 적용해서 유효 값인지 아닌지 확인
      //   return value === '1' || value === '0';
      // },
    },
  },
  // 컴포넌트에 연결해줘야하는 props는 카멜케이스로! + 커스텀 속성 (required등) 을 추가해줘야 이용 가능
  emits: ['onToogle-favorite', 'delete'],
  //  emits: {
  //     'onToogle-favorite': function (id) {
  //       if (id) {
  //         return true;
  //       } else {
  //         console.warn('Id is missing!');
  //         return false;
  //       }
  // },
  // },
  //커스텀 이벤트 정의 : for understanding code, 팀작업을 할 때 유용하며 props처럼 정의도 가능
  // id를 인수로 보내는 위의 함수 같은 경우는 id가 있는지에 따라 ture/false를 리턴할 수 있음
  data() {
    return {
      detailsAreVisible: false,
      // friend: {
      //   id: 'manuel',
      //   name: 'Manuel Lorenz',
      //   phone: '0123 45678 90',
      //   email: 'manuel@localhost.com',
      // },
      // friendIsFavorite: true,
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toogleFavorite() {
      this.$emit('onToogle-favorite', this.id);
      //이벤트는 케밥케이스로만 사용
      // $emit 메서드로 컴포넌트 내부에서 커스텀 이벤트를 발생시키면서 첫번째 인수 id를 전달
    },
  },
};
</script>
