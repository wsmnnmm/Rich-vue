<template>
  <div>
    <label class="notes">
      {{ value }}
      <span class="name">备注</span>
      <input type="text" :value="value"
             @input="onInput"
             placeholder="在这输入备注">
    </label>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';

@Component

export default class Notes extends Vue {
  value = '';

  onInput(event: KeyboardEvent) {
    const input = event.target as HTMLInputElement;
    this.value = input.value;
  }
}
</script>

<style lang="scss" scoped>
.notes {
  background: #f5f5f5;
  font-size: 14px;
  display: flex;
  padding-left: 16px;
  align-items: center;

  .name {
    padding-right: 16px;
  }

  input {
    flex-grow: 1;
    height: 64px;
    background: transparent;
    border: none;
    padding-right: 16px;
  }
}
</style>