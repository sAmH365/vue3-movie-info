<template>
  <Navbar />
  <Event :text="text" />
  <SearchBar :data="data_tmp" @searchMovie="searchMovie($event)"/>
  <p>
    <button @click="showAllMovie">전체보기</button>
  </p>
  <Movies
      :data="data_tmp"
      @openModal="isModal=true;selectedMovie=$event"
      @increaseLike="increseLike($event)"
  />
  <Modal
      :data="data_tmp"
      :isModal="isModal"
      :selectedMovie="selectedMovie"
      @closeModal="isModal=false"
  />

</template>

<script>
import data from './assets/movies'; // 영화 데이터
import Navbar from './components/Navbar.vue';
import Event from './components/Event.vue'; // 이벤트 박스
import Modal from './components/Modal.vue';
import Movies from './components/Movies.vue';
import SearchBar from "@/components/SearchBar.vue"; // 검색창

export default {
  name: 'App',
  data() {
    return {
      isModal: false,
      data,
      data_tmp: [...data], // 사본
      selectedMovie: 0,
      text: "NETPLIX 강렬한 운명의 드라마, 경기크리처"
    }
  },
  methods: {
    increseLike(i) {
      this.data[i].like += 1;
    },
    searchMovie(title) {
      // 영화제목이 포함된 데이터를 가져옴
      this.data_tmp = this.data.filter(movie => {
        return movie.title.includes(title);
      })
    },
    showAllMovie() {
      this.data_tmp = this.data;
    }
  },
  components: {
    Navbar,
    Event,
    Modal,
    Movies,
    SearchBar
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
</style>