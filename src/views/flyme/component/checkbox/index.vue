<template>
  <div class="mzui-demo">
    <scroller class="scroller">
      <title></title>
      <category title="单独使用"></category>
        <fm-checkbox
          v-bind="{ title: '单行信息' }"
          @fmCheckboxChecked="check"></fm-checkbox>
        <fm-checkbox
          v-bind="{ title: '烧花鸭', imgSrc: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=995362387,2344079991&fm=27&gp=0.jpg' }"
          @fmCheckboxChecked="check"></fm-checkbox>
        <fm-checkbox
          v-bind="{ title: '烧雏鸡', summary: '挺好吃的，帮你先选了', imgSrc: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=995362387,2344079991&fm=27&gp=0.jpg' }"
          checked
          @fmCheckboxChecked="check"></fm-checkbox>
        <fm-checkbox
          v-bind="{ title: '松花小肚儿', summary: '一定要吃这个，不能不选', description: '肯定比上面的好吃', imgSrc: 'https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=995362387,2344079991&fm=27&gp=0.jpg' }"
          checked
          disabled
          @fmCheckboxChecked="check"></fm-checkbox>

      <category title="组合使用"></category>
        <fm-checkbox-list
          :list="list"
          @fmCheckBoxListChecked="onChecked1"></fm-checkbox-list>
        <text class="checked-text">选中项 {{(checkedList1.map(item => item.title)).toString()}}</text>

      <category title="单选模式"></category>
        <fm-checkbox-list
          single
          :list="list"></fm-checkbox-list>

      <category title="限制选中数量"></category>
        <fm-checkbox-list
          :list="list"
          limit="2"
          @overLimit="overLimit"
          @fmCheckBoxListChecked="onChecked2"></fm-checkbox-list>
        <text class="checked-text">选中项 {{(checkedList2.map(item => item.title)).toString()}}</text>
    </scroller>
  </div>
</template>

<style scoped>
  .mzui-demo {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    background-color: #ffffff;
  }

  .container {
    padding-top: 60px;
    padding-left: 60px;
    padding-right: 60px;
  }

  .row {
    flex-direction: row;
    flex-wrap: wrap;
  }

  .btn {
    margin-right: 60px;
  }

  .scroller {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
  }

  .demo-content {
		height: 840px;
  }

  .checked-text {
    font-size: 42px;
    color: #333333;
    margin-top: 30px;
    margin-bottom: 30px;
    margin-left: 24px;
  }
</style>

<script>
  import { FmCheckbox, FmCheckboxList } from 'weex-flymeui'
  import Title from '@components/flyme/_mods/title.vue'
  import Category from '@components/flyme/_mods/category.vue'

  const modal = weex.requireModule('modal')

  export default {
    components: { Title, Category, FmCheckbox, FmCheckboxList },
    data: () => ({
      list: [{
        title: '选项1',
        value: 0
      }, {
        title: '选项2',
        value: 1,
        summary: '描述'
      }, {
        title: '选项3',
        value: 2,
        summary: '描述',
        description: '段落描述'
      }],
      checkedList1: [],
      checkedList2: []
    }),
    methods: {
      onChecked1 (e) {
        this.checkedList1 = e.checkedList
      },
      onChecked2 (e) {
        this.checkedList2 = e.checkedList
      },
      overLimit (e) {
        modal.toast({ message: '超过' + e + '个了' })
      }
    }
  }
</script>
