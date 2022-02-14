<template>
  <Layout class-prefix="layout">
    <Tags :value.sync="record.tags"/>
    <FormItem
        field-name="备注"
        placeholder="请输入备注"
        :value="record.notes" @update:value="onUpdateNotes($event)"/>
    <Tabs :data-source="recordTypeList" :value.sync="record.type"/>
    <NumberPad :value.sync="record.amount" @submit="saveRecord"/>
  </Layout>
</template>

<script lang="ts">
import Vue from 'vue';
import NumberPad from '@/components/Money/NumberPad.vue';
import Tags from '@/components/Money/Tags.vue';
import {Component} from 'vue-property-decorator';
import Tabs from '@/components/Tabs.vue';
import recordTypeList from '@/constants/recordTypeList';
import FormItem from '@/components/Money/FormItem.vue';

@Component({
  components: {Tabs, Tags, FormItem, NumberPad},
})
export default class Money extends Vue {
  get recordList() {
    return this.$store.state.recordList;
  }

  recordTypeList = recordTypeList;

  record: RecordItem = {
    tags: [],
    notes: '',
    type: '-',
    amount: 0,
  };

  created() {
    this.$store.commit('fetchRecords');
  }

  onUpdateNotes(value: string) {
    this.record.notes = value;
  }

  saveRecord() {
    if (!this.record.tags || this.record.tags.length === 0) {
      return window.alert('请至少选择一个标签');
    }
    this.$store.commit('createRecord', this.record);
    this.record.notes = '';
    this.record.amount = 0;
    console.log(this.record);
    window.alert('已保存');
  }
}
</script>

<style lang="scss">
.layout-content {
  background-color: #fff;
  display: flex;
  flex-direction: column;
}
</style>
<style lang="scss" scoped>
@import "~@/assets/style/helper";
</style>
