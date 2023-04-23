<template>
  <div style="padding: 50px;">
    <div style="margin-bottom: 20px;">点击按钮显示组件</div>
    <el-button v-for="(item,index) in btnList" style="margin-bottom: 20px;" type="success" @click="btnIndex=index">{{ item.title }}</el-button>
  <div v-if="btnIndex===0"><cascader :cascaderInfo="cascaderInfo"></cascader></div>
  <div v-if="btnIndex===1"><dateTimePiker :dateTimePikerInfo="dateTimePikerInfo"></dateTimePiker></div>
  <div v-if="btnIndex===2"><select :selectInfo="selectInfo"></select></div>
  <div v-if="btnIndex===3"><radio :radioInfo="radioInfo"></radio></div>
  <div v-if="btnIndex===4"><editor :edtorInfo="edtorInfo"></editor></div>
  <div v-if="btnIndex===5"><checkbox :checkboxInfo="checkboxInfo"></checkbox></div>
  <div v-if="btnIndex===6"><tableCom :tableType="tableType"></tableCom></div>
  <div v-if="btnIndex===7"><pagenation :currentPage="4" :pageSizes="2" :pageSize="3" :total="total"></pagenation></div>
  </div>
</template>

<script>
import editor from './components/editor.vue'
import radio from './components/radio.vue'
import checkbox from './components/checkbox.vue'
import select from './components/select.vue'
import cascader from './components/cascader.vue'
import dateTimePiker from './components/dateTimepiker.vue'
import tableCom from './components/table.vue'
import pagenation from './components/pagenation.vue'
export default {
  name: 'mytools',
  components: {
    editor,
    radio,
    checkbox,
    select,
    cascader,
    dateTimePiker,
    tableCom,
    pagenation
  },
  data () {
    return {
      btnIndex:null,
      btnList:[
        {title:'二次封装级联选择器',},
        {title:'二次封装时间选择器',},
        {title:'二次封装下拉选择器',},
        {title:'二次封装单选组件',},
        {title:'二次富文本编辑器',},
        {title:'二次封装多选',},
        {title:'二次封装表格',},
        {title:'二次封装分页',},
      ],
      edtorInfo: '富文本编辑器信息',
      radioInfo: '单选信息',
      checkboxInfo: '多选信息',
      selectInfo: '下拉选择信息',
      cascaderInfo: '级联选择器信息',
      dateTimePikerInfo: '时间选择信息',
      tableType: [
        { type: 'index', width: '100' },
        { prop: 'date', label: '日期', width: '100' },
        { prop: 'name', label: '姓名', width: '100' },
        { prop: 'address', label: '地址', width: '100' },
        { prop: '', label: '操作', width: '180' }
      ],
    }
  },
  mounted () {
  },
  methods: {
  }
}
</script>

<style lang="less" scoped>
</style>
