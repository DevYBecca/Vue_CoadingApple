<template>
  <Transition name="fade">
    <Modal
      @closeModal="모달창열렸니 = false"
      :원룸들="원룸들"
      :누른거="누른거"
      :모달창열렸니="모달창열렸니"
    />
  </Transition>

  <div class="menu">
    <a v-for="작명 in 메뉴들" :key="작명">{{ 작명 }}</a>
  </div>

  <Discount v-if="showDiscount == true" />

  <button @click="priceSort">가격 순 정렬</button>
  <button @click="sortBack">되돌리기</button>

  <Card
    @openModal="
      모달창열렸니 = true;
      누른거 = $event;
    "
    :원룸="원룸들[i]"
    v-for="(원룸, i) in 원룸들"
    :key="원룸"
  />
</template>

<script>
import data from './assets/oneroom';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';

export default {
  name: 'App',
  data() {
    return {
      showDiscount: true,
      원본원룸들: [...data],
      누른거: 0,
      원룸들: data,
      모달창열렸니: false,
      신고수: [0, 0, 0],
      메뉴들: ['Home', 'Shop', 'About'],
      products: ['역삼동원룸', '천호동원룸', '마포구원룸'],
    };
  },
  methods: {
    increase() {
      this.신고수 += 1;
    },
    sortBack() {
      this.원룸들 = [...this.원본원룸들];
    },
    priceSort() {
      this.원룸들.sort(function (a, b) {
        return a.price - b.price;
      });
    },
  },
  mounted() {
    setTimeout(() => {
      this.showDiscount = false;
    }, 2000);
  },
  components: {
    Discount,
    Modal,
    Card,
  },
};
</script>

<style>
.fade-leave-from {
  opacity: 1;
}

.fade-leave-active {
  transition: all 1s;
}

.fade-leave-to {
  opacity: 0;
}

.fade-enter-from {
  transform: translateY(-1000px);
}

.fade-enter-active {
  transition: all 1s;
}

.fade-enter-to {
  transform: translateY(0px);
}

body {
  margin: 0;
}

div {
  box-sizing: border-box;
}

.discount {
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
  background-color: #eee;
}

.black-bg {
  position: fixed;
  padding: 20px;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.white-bg {
  padding: 20px;
  width: 100%;
  border-radius: 8px;
  background-color: white;
}

.room-img {
  margin-top: 40px;
  width: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  padding: 15px;
  border-radius: 5px;
  background-color: darkslateblue;
}

.menu a {
  padding: 10px;
  color: white;
}
</style>
