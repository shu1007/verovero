
<template>
  <div id="app" :class="levelClass">
    <h2>よっぱらいレベル</h2>
    <div>
      <div class="level-box">
        <span class="level">{{level}}</span>
        <span class="bero">ベロベロ</span>
      </div>
    </div>
    <img class="people" alt="image" :src="path" />
    <button type="button" v-if="level > 99"></button>
  </div>
</template>


<script>
import Axios from "axios";
import "../node_modules/ress/dist/ress.min.css";

export default {
  name: "app",
  data() {
    return {
      level: 0
    };
  },
  mounted() {
    setInterval(() => {
      const self = this;
      // MEMO : 0.5秒ごとにAPIを叩く
      Axios.get("http://localhost:3000/tableData").then(res => {
        self.level = res.data[0].data;
      });
    }, 500);
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
    },
    levelClass: function() {
      const l = this.level;
      if (l == 100) {
        return "level-100";
      } else if (l >= 80) {
        return "level-80";
      } else {
        return "level-normal";
      }
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #b7d3f5;
  margin: 0;
  width: 100%;
  height: 100vh;
  h2 {
    width: 100vw;
    font-size: 52px;
    text-align: center;
    padding-top: 180px;
  }
  .level-box {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 40px;
  }
  .level {
    width: 300px;
    background: #fff;
    flex: none;
    display: block;
    font-size: 130px;
    text-align: center;
    line-height: 1.2em;
  }
  .bero {
    font-size: 40px;
    margin-left: 20px;
    font-weight: bold;
  }

  .people {
    width: 220px;
    display: block;
    margin: 40px auto;
  }

  &.level-normal {
    background: #b7d3f5;
  }

  &.level-80 {
    background: #f8de62;
  }

  &.level-100 {
    background: #f86262;
    background-image: url("../images/fire.png");
    background-size: 100% auto;
    background-repeat: no-repeat;
    background-position: bottom 0 right 0;
  }

  button {
    position: absolute;
    width: 600px;
    height: 200px;
    display: block;
    background-image: url("../images/button.png");
    background-size: contain;
    background-repeat: no-repeat;
    bottom: 40px;
    left: 50%;
    transform: translateX(-50%);
  }
}
</style>
