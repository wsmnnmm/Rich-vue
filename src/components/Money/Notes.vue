<template>
  <div>
    <label class="notes">
      <span class="name">备注</span>
      <input type="text"
             v-model="value"
             placeholder="在这输入备注">
    </label>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component, Watch} from 'vue-property-decorator';

@Component

export default class Notes extends Vue {
  value = '';

  @Watch('value')
  onValueChanged(value: string) {
    this.$emit('update:value', value);
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