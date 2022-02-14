<template>
  <div class="tags">
    <ul class="current">
      <li
          v-for="tag in tagList"
          :key="tag.id"
          :class="{ selected: selectedTags.indexOf(tag) >= 0 }"
          @click="toggle(tag)"
      >
        {{ tag.name }}
      </li>
    </ul>
    <div class="new">
      <button @click="createTag">新增标签</button>
    </div>
  </div>
</template>

<script lang="ts">
import {Component} from 'vue-property-decorator';
import {mixins} from 'vue-class-component';
import TagHelper from '@/mixins/TagHelper';

@Component
export default class Tags extends mixins(TagHelper) {
  selectedTags: string[] = [];

  get tagList() {
    return this.$store.state.tagList;
  }

  created() {
    this.$store.commit('fetchTags');
  }

  toggle(tag: string) {
    const index = this.selectedTags.indexOf(tag);
    if (index >= 0) {
      this.selectedTags.splice(index, 1);
    } else {
      this.selectedTags.push(tag);
    }
    this.$emit('update:value', this.selectedTags);
  }
}
</script>

<style lang="scss" scoped>
@import "~@/assets/style/helper";

.tags {
  background: white;
  display: flex;
  flex-grow: 1;
  font-size: 14px;
  padding: 16px;
  flex-direction: column;
  justify-content: space-between;
  overflow: auto;

  > .current {
    display: flex;
    flex-wrap: wrap;

    > li {
      $bg: #dbfcf4;
      background: $bg;
      $h: 24px;
      height: $h;
      line-height: $h;
      color: $themeColor;
      padding: 0 16px;
      border-radius: $h/2;
      margin-right: 12px;
      margin-top: 10px;

      &.selected {
        color: white;
        background: darken($bg, 30%);
        background-color: $themeColor;
      }
    }
  }

  > .new {
    padding-top: 16px;

    button {
      background: transparent;
      border: none;
      color: $themeColor;
      border-bottom: 1px solid;
      padding: 0 4px;
    }
  }
}
</style>