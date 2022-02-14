<template>
  <div class="tip" v-if="value">
    <div class="mask" @click="closeTip"></div>
    <div class="qrcode">
      <div class="closeBtn" @click="closeTip">×</div>
      <!--      <img src="@/assets/img/qrcode.png" alt="图片">-->
      <div>手机扫码体验更佳</div>
    </div>
  </div>
</template>
<script lang="ts">
import Vue from 'vue';
import {Component, Prop} from 'vue-property-decorator';

@Component
export default class Qrcode extends Vue {
  @Prop(Boolean) value = true;

  closeTip() {
    this.$emit('update:value', false);
  }
}
</script>
<style lang="scss">

.tip {
  .closeBtn {
    position: absolute;
    top: 0;
    right: 0;
    width: 30px;
    height: 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    border-radius: 50%;

    &:hover {
      background-color: rgba(0, 0, 0, 0.15);
    }
  }

  .mask {
    width: 100vw;
    height: 100vh;
    background-color: rgba(0, 0, 0, 0.5);
  }

  .qrcode {
    box-shadow: 0 0 5px 5px #777;
    padding: 20px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 10px;
    overflow: hidden;
    background-color: #fff;
    width: 200px;
    text-align: center;

    img {
      width: 100%;
    }
  }

  .mask {
    position: fixed;
    top: 0;
    left: 0;
  }
}
</style>
