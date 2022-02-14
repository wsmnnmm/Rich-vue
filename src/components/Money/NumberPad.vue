<template>
  <div class="numberPad">
    <div class="output">{{ output }}</div>
    <div class="buttons">
      <button @click="inputContent">1</button>
      <button @click="inputContent">2</button>
      <button @click="inputContent">3</button>
      <button @click="remove">删除</button>
      <button @click="inputContent">4</button>
      <button @click="inputContent">5</button>
      <button @click="inputContent">6</button>
      <button @click="clear">清空</button>
      <button @click="inputContent">7</button>
      <button @click="inputContent">8</button>
      <button @click="inputContent">9</button>
      <button @click="ok" class="ok">OK</button>
      <button @click="inputContent" class="zero">0</button>
      <button @click="inputContent">.</button>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component, Prop} from 'vue-property-decorator';

@Component
export default class NumberPad extends Vue {
  @Prop(Number) readonly value!: number;
  output = this.value.toString();

  inputContent(event: MouseEvent) {
    const button = event.target as HTMLButtonElement;
    const input = button.textContent!;
    if (this.output.length === 16) {
      return;
    }
    if (this.output === '0') {
      if ('0123456789'.indexOf(input) >= 0) {
        this.output = input;
      } else {
        this.output += input;
      }
      return;
    }
    if (this.output.indexOf('.') >= 0 && input === '.') {
      return;
    }
    this.output += input;
  }

  remove() {
    if (this.output.length === 1) {
      this.output = '0';
    } else {
      this.output = this.output.slice(0, -1);
    }
  }

  clear() {
    this.output = '0';
  }

  ok() {
    const number = parseFloat(this.output);
    this.$emit('update:value', number);
    this.$emit('submit', number);
    this.output = '0';
  }
}
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper.scss";

.numberPad {
  .output {
    font-size: 40px;
    font-family: Consolas, monospace;
    padding: 9px 16px;
    box-shadow: inset 0 -5px 5px -5px #f5f5f5, inset 0 5px 5px -5px #f5f5f5;
    height: 72px;
  }

  .buttons {
    > button {
      @extend %clearFix;
      $button_height: 64px;
      $button_width: 25%;
      float: left;
      width: $button_width;
      height: 64px;
      background-color: transparent;
      border: none;
      border-left: 1px solid #ddd;
      border-top: 1px solid #ddd;

      &:active {
        background-color: $themeColor;
        color: #fff;
      }

      &.ok {
        float: right;
        height: $button_height * 2;
      }

      &.zero {
        width: $button_width * 2;
      }

      $bg: #f5f5f5;
      $inc: 6%;

      &:nth-child(4),
      &:nth-child(8) {
        color: $themeColor;
        background-color: $themeColor-light;
        border-right: 1px solid #ddd;
      }

      &:nth-child(12) {
        color: white;
        background-color: $themeColor;
        border-bottom: 1px solid #ddd;
        border-right: 1px solid #ddd;
      }

      &:nth-child(13),
      &:nth-child(14) {
        border-bottom: 1px solid #ddd;
      }
    }
  }
}
</style>