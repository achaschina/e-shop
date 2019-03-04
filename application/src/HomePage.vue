<template>
  <div>
    <b-jumbotron id="home-page" :header="msg" lead>
      <!-- <p>Для просмотра детальной информации по заказу войдите в личный кабинет</p>
      <b-btn variant="secondary" to="/category" style="margin-bottom:1rem;">Категории</b-btn>-->
      <carousel :perPage="1" :autoplay="true">
        <slide v-for="(pic, index) in sliderPics" v-bind:key="index">
          <img :src="getImg(index)">
        </slide>
      </carousel>
    </b-jumbotron>
    <!-- <div class="questions" @click="haveQuestion=true;" >
      <form :class="{ active : haveQuestion}">
        <div style="float: right; vertical-align: middle">
          <p style="cursor: pointer; font-size: 29px; color: #d8d8d8" @click="showQuestionSForm">
            <font-awesome-icon :icon="['fas', 'window-close']" />
          </p>
        </div>
      </form>
    </div>-->
    <div class="questions" :class="{ active : haveQuestion}">
      <div class="relative">
        <font-awesome-icon
          class="writeMeIcon"
          :icon="['fas', 'pencil-alt']"
          @click="haveQuestion=true;"
        />
        <font-awesome-icon
          class="closeIcon"
          :icon="['fas', 'window-close']"
          @click="haveQuestion=false;"
        />
        <b-form>
          <h3>Напишите мне</h3>
          <b-form-group
            id="nameGroup"
            label="Имя:"
            label-for="name"
            description=""
          >
            <b-form-input
              id="name"
              type="text"
              v-model="form.name"
              required
              placeholder=""
            />
          </b-form-group>
          <b-form-group
            id="emailGroup"
            label="Почта:"
            label-for="email"
            description=""
          >
            <b-form-input
              id="email"
              type="email"
              v-model="form.email"
              required
              placeholder=""
            />
          </b-form-group>
          <b-form-group
            id="questionGroup"
            label="Вопрос:"
            label-for="question"
          >
            <b-form-textarea
              id="question"
              v-model="form.text"
              placeholder=""
            />
          </b-form-group>
          <b-button @click="sendQuestion">Отправить</b-button>
        </b-form>
      </div>
    </div>
  </div>
</template>

<script>
import data from "./utilities/testData.js";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
export default {
  name: "app",
  components: {
    FontAwesomeIcon
  },
  data() {
    return {
      msg: "",
      form: {
        name: '',
        email: '',
        text: ''
      },
      sliderPics: data.mainPageSlider,
      haveQuestion: false
    };
  },
  mounted() {},
  methods: {
    sendQuestion() {
      console.log(this.form);
    },
    getImg(i) {
      let imgUrl = data.mainPageSlider[i].url;
      return imgUrl ? require(`${imgUrl}`) : "";
    },
    showQuestionSForm() {
      this.haveQuestion = false;
      console.log(this.haveQuestion);
    }
  }
};
</script>

<style scoped>
.btn-secondary {
    color: #fff;
    background-color: #be9e56;
    border-color: #be9e56;
}
.btn {
  width: 100%;
  border-radius: 0;
}
.form-control {
  border-radius: 0 !important;
  border: none;
}
.form-control:focus {
    outline: 0;
    box-shadow: none;
}
textarea.form-control {
    min-height: 100px;
}
.questions > form {
  position: absolute;
  width: 15rem;
  background: #f3f2f2;
  z-index: 10000000;
  min-height: 20rem;
  padding: 0 0.5rem 1rem 1rem;
  left: -16rem;
}
.questions.active {
  left: 0;
}

.questions.active .relative .writeMeIcon {
  display: none;
}

.questions {
  position: fixed;
  left: -300px;
  top: 35%;
  z-index: 10010;
  transition: all 0.5s ease;
  -webkit-transition: all 0.5s ease;
}
.relative {
  position: relative;
  padding: 15px;
  width: 300px;
  background-color: #e5e5e5;
  zoom: 1;
  min-height: 15rem;
}
.questions .relative .writeMeIcon {
  color: white;
  background-color: #979797;
  width: 50px;
  height: 50px;
  position: absolute;
  top: 0;
  padding: 10px;
  right: -50px;
  transition: all 0.3s ease;
  -webkit-transition: all 0.3s ease;
}
.questions .relative .writeMeIcon:hover {
  background-color: #be9e56;
}
.closeIcon {
  cursor: pointer;
  font-size: 29px;
  color: #979797;
  float: right;
}
.relative {
  font-family: "Oswald", sans-serif;
}
.relative h3 {
  font-size: 16px;
  font-weight: 700;
  margin-bottom: 20px;
}
</style>
