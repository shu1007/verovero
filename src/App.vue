
<template>
  <div id="app">
    <h2>よっぱらいレベル</h2>
    <div>
      <span class="level">{{level}}</span>
      <span>レベル</span>
    </div>
    <img alt="image" :src="path" />
    <button type="button" v-if="level > 99">チェイサー</button>
  </div>
</template>

<script>
import Axios from "axios";

export default {
  name: "app",
  data() {
    return {
      level: 10
      // path: require("../images/people_50.png")
    };
  },
  mounted() {
    setInterval(() => {
      const self = this;
      // MEMO : 0.5秒ごとにAPIを叩く
      Axios.get("http://localhost:3000/tableData").then(res => {
        self.level = res.data[0].data;
      });
    }, 1000);
  },
  computed: {
    path: function() {
      const l = this.level;
      if (l == 100) {
        return require("../images/people_100.png");
      } else if (l >= 80) {
        return require("../images/people_80.png");
      } else {
        return require("../images/people_50.png");
      }
    }
  }
  // compotents: { ImagePic, HelloWorld }
};
</script>

<style>
/* #app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
</style>
