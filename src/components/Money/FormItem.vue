<template>
  <div>
    <label class="formItem">
      <span class="name">{{ this.fieldName }}</span>
      <input
        type="text"
        :value="value"
        @input="onValueChanged($event.target.value)"
        :placeholder="this.placeholder"
      />
    </label>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop } from "vue-property-decorator";

@Component
export default class FormItem extends Vue {
  @Prop({ default: "" }) readonly value!: string;

  @Prop({ required: true }) fieldName!: string;
  @Prop() placeholder?: string;

  onValueChanged(value: string) {
    this.$emit("update:value", value);
  }
}
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper";
.formItem {
  background-color: #fff;
  padding: 0 16px;
  display: flex;
  align-items: center;

  .name {
  }

  input {
    margin-left: 16px;
    height: 64px;
    flex-grow: 1;
    background-color: transparent;
    border: none;
  }
}
</style>