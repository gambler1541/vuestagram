<template>
  <div class="header">
      <ul class="header-button-left">
        <li>Cancel</li>
      </ul>
      <ul class="header-button-right">
        <li @click="nextStep" v-if="this.step == 1">Next</li>
        <li @click="publish" v-if="this.step == 2">발행</li>
      </ul>
      <img src="./assets/logo.png" class="logo" />
  </div>
  <container-view :data="data" :imgUrl="imgUrl" :step="step" @write="this.myPostContent = $event"></container-view>
  <button @click="more">더보기</button>
  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" />
      <label for="file" class="input-plus">+</label>
    </ul>
  </div>
  <!-- <div v-if=" tab == 1">탭1</div>
  <div v-if=" tab == 2">탭2</div>
  <div v-if=" tab == 3">탭3</div>
  <button @click="this.tab = 1">탭1</button>
  <button @click="this.tab = 2">탭2</button>
  <button @click="this.tab = 3">탭3</button> -->
</template>

<script>
import ContainerView from './components/ContainerView.vue'
import data from './assets/data/data'
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      data : data,
      imgUrl : '',
      page : 0,
      step : 0,
      myPostContent : '',
    }
  },
  components: {
    ContainerView,
  },
  methods: {
    more() {
      axios.get(`https://codingapple1.github.io/vue/more${this.page}.json`)
        .then(res=> {
          this.data.push(res.data);
          this.page += 1;
        })
        .catch(e => console.log(e));
    },
    upload(e) {
      let file = e.target.files;
      this.imgUrl = URL.createObjectURL(file[0]);
      this.step = 1;
    },
    nextStep() {
      this.step += 1;
    },
    publish() {
      let myPost = {
        name: 'park',
        userImage: 'https://placeimg.com/100/100/arch',
        postImage: this.imgUrl,
        likes: 0,
        date: 'May 15',
        liked: false,
        content: this.myPostContent,
        filter: 'perpetua'
      };
      this.data.unshift(myPost);
      this.step = 0;   
    }
  }
}
</script>

<style>
  body {
      margin: 0;
  }

  ul {
      padding: 5px;
      list-style-type: none;
  }

  .logo {
      width: 22px;
      margin: auto;
      display: block;
      position: absolute;
      left: 0;
      right: 0;
      top: 13px;
  }

  .header {
      width: 100%;
      height: 40px;
      background-color: white;
      padding-bottom: 8px;
      position: sticky;
      top: 0;
  }

  .header-button-left {
      color: skyblue;
      float: left;
      width: 50px;
      padding-left: 20px;
      cursor: pointer;
      margin-top: 10px;
  }

  .header-button-right {
      color: skyblue;
      float: right;
      width: 50px;
      cursor: pointer;
      margin-top: 10px;
  }

  .footer {
      width: 100%;
      position: sticky;
      bottom: 0;
      padding-bottom: 10px;
      background-color: white;
  }

  .footer-button-plus {
      width: 80px;
      margin: auto;
      text-align: center;
      cursor: pointer;
      font-size: 24px;
      padding-top: 12px;
  }

  .sample-box {
      width: 100%;
      height: 600px;
      background-color: bisque;
  }

  .inputfile {
      display: none;
  }

  .input-plus {
      cursor: pointer;
  }

  #app {
      box-sizing: border-box;
      font-family: "consolas";
      margin-top: 60px;
      width: 100%;
      max-width: 460px;
      margin: auto;
      position: relative;
      border-right: 1px solid #eee;
      border-left: 1px solid #eee;
  }
</style>
