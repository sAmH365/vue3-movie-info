<template>
  <NavBar />
  <Event :text="text"/>
<h1>영화정보</h1>
<div v-for="(movie, i ) in data" :key="i" class="item">
  <figure>
    <img :src="`${movie.imgUrl}`" :alt="movie.title">
  </figure>

  <div class="info">
    <h3 class="bg-yellow">{{ movie.title }}</h3>
    <p>{{ movie.year }}</p>
    <p>{{ movie.category }}</p>
    <button @click="increaseLike(i)">좋아요</button> <span> {{ movie.like }}</span>
    <p>
      <button @click="isModal=true; selectedMovie=i">상세정보</button>
    </p>
  </div>

  <Modal />
</div>
</template>

<script>
import { data } from './assets/movies'
import NavBar from "@/components/NavBar.vue";
import Modal from "@/components/Modal.vue";
import Event from "@/components/Event.vue";

export default {
  name: 'App',
  data() {
    return {
      isModal: false,
      data,
      selectedMovie: 0,
      text: 'NETPLIX 강렬한 운명의 드라마, 경기크리처'
    }
  },
  methods: {
    increaseLike(index) {
      this.data[index].like += 1;
    }
  },
  components: {
    NavBar,
    Modal,
    Event
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}

body {
  max-width: 768px;
  margin: 0 auto;
}

h1,
h2,
h3 {
  margin-bottom: 1rem;
}

p {
  margin-bottom: 0.5rem;
}

button {
  margin-right: 10px;
  margin-top: 1rem;
}

.item {
  width: 100%;
  border: 1px solid #ccc;
  display: flex;
  margin-bottom: 20px;
  padding: 1rem;
}

.item figure {
  width: 30%;
  margin-right: 1rem;
}

.item img {
  width: 100%;
}

.item .info {
  width: 100%;
}

.modal {
  background: rgba(0, 0, 0, 0.7);
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal .inner {
  background: #fff;
  width: 80%;
  padding: 20px;
  border-radius: 10px;
}

p:has(.btn-all) {
  text-align: center;
}
</style>