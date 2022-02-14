<template>
  <div id="app">
    <router-view/>
    <button class="btn" @click="showQrcode">手机扫一扫</button>
    <Qrcode class="qrcode" :value.sync="QrcodeVisible"/>
  </div>
</template>
<script>
import Vue from "vue";
import Component from "vue-class-component";
import Qrcode from "@/components/Qrcode";

@Component({
  components: {Qrcode}
})
export default class App extends Vue {
  QrcodeVisible = true;

  showQrcode() {
    this.QrcodeVisible = true
  }
}
</script>
<style lang="scss">
@import "~@/assets/style/reset.scss";
@import "~@/assets/style/helper.scss";

body {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #333;
  line-height: 1.5;
  font-size: 16px;
  font-family: $font-hei;
  background: #f5f5f5;
}

#app {
  max-width: 425px;
  margin: 0 auto;
  box-shadow: 0 0 5px 2px rgba(0, 0, 0, 0.2);
}

.btn {
  border: none;
  background-color: $themeColor;
  color: white;
  padding: 2px 10px;
  border-radius: 10px;
  position: absolute;
  left: 50%;
  bottom: 0;
  transform: translateX(212.5px);
  margin-left: 5px;
}
</style>
