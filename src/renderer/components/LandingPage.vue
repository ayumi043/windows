<template>
  <div id="wrapper">
    <h2>Screen Brightness</h2>
    <main>
      <el-slider v-model="light" @input="change"></el-slider>
      <p>
        <el-switch
          v-model="value"
          inactive-text="night"
          active-color="#13ce66"
          inactive-color="#ff4949"
          @change="change"
        ></el-switch>
      </p>
    </main>
  </div>
</template>

<script>
import SystemInformation from "./LandingPage/SystemInformation";
const { ipcRenderer } = require("electron");
export default {
  name: "landing-page",
  components: { SystemInformation },
  data() {
    return {
      light: 50,
      value: true
    };
  },
  methods: {
    change() {
      let v = this.light;
      if (this.value) {
        v = this.light * -1;
      }
      ipcRenderer.send("light", v);
      console.log(this.light);
    },
    open(link) {
      this.$electron.shell.openExternal(link);
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Source Sans Pro", sans-serif;
}

#wrapper {
  background: radial-gradient(
    ellipse at top left,
    rgba(255, 255, 255, 1) 40%,
    rgba(229, 229, 229, 0.9) 100%
  );
  height: 100vh;
  padding: 60px 80px;
  width: 100vw;
}

#logo {
  height: auto;
  margin-bottom: 20px;
  width: 420px;
}

main {
  display: flex;
  justify-content: space-between;
}

main > div {
  flex-basis: 50%;
}

.left-side {
  display: flex;
  flex-direction: column;
}

.welcome {
  color: #555;
  font-size: 23px;
  margin-bottom: 10px;
}

.title {
  color: #2c3e50;
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 6px;
}

.title.alt {
  font-size: 18px;
  margin-bottom: 10px;
}

.doc p {
  color: black;
  margin-bottom: 10px;
}

.doc button {
  font-size: 0.8em;
  cursor: pointer;
  outline: none;
  padding: 0.75em 2em;
  border-radius: 2em;
  display: inline-block;
  color: #fff;
  background-color: #4fc08d;
  transition: all 0.15s ease;
  box-sizing: border-box;
  border: 1px solid #4fc08d;
}

.doc button.alt {
  color: #42b983;
  background-color: transparent;
}
</style>
