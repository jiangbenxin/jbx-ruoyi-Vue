<template>
  <div style="padding: 50px;">
  <div style="margin-bottom: 20px;">npm run 加第三方包名下载第三方包可以下载淘宝镜像npm install -g cnpm --registry=https://registry.npm.taobao.org，cnpm -v，npm i yarn</div>
  <div style="margin-bottom: 20px;">点击按钮显示组件</div>

  <el-button v-for="(item,index) in btnList" style="margin-bottom: 20px;" type="success" @click="btnIndex=index">{{ item.title }}</el-button>
  <div v-if="btnIndex==0">npm i jsmd5  {{$md5("这里编写你加密的东西")}}</div>
  <div v-if="btnIndex==1">npm i jssha256   {{ $sha256('2222') }}</div>
  <div v-if="btnIndex==2">npm i dayjs  <el-button type="success" plain @click="timeFilter()">DD/MM/YYYY</el-button>，{{date1}}</div>
  <div v-if="btnIndex==3">npm i lodash  <el-button type="info" plain @click="fangdou()">防抖</el-button><el-button type="info" plain @click="jieliu()">节流</el-button></div>
  <div v-if="btnIndex==4">npm i qrcode  <img :src="QRImgUrl" /></div>
  <div v-if="btnIndex==5">npm i vue-amap  <vueAmap></vueAmap></div>
  </div>
</template>

<script>
import dayjs from 'dayjs'
import QRCode from 'qrcode'
import _ from 'lodash'
import vueAmap from './vue-amap/index.vue'

export default {
  name: 'mytools',
  components: {
    vueAmap
  },
  data () {
    return {
      btnIndex:null,
      btnList:[
        {title:'md5加密',},
        {title:'sha256加密：',},
        {title:'format时间格式转换',},
        {title:'防抖节流',},
        {title:'qrcodejs生成二维码',},
        {title:'vueAmap高德地图组件',},
      ],
      date1: '2019-01-25',
      QRImgUrl: '',
    	QRlink:'www.baidu.com'
    }
  },
  mounted () {
    // this.creatQrCode()
    // this.toTree()
    this.getQRcode()
  },
  methods: {
    // 防抖
    fangdou: _.debounce(() => {
      console.log('防抖')
    }, 1000),
    // 节流
    jieliu: _.throttle(() => {
      console.log('节流')
    }, 3000),
    // 时间过滤
    timeFilter () {
      this.date1 = dayjs(this.date1).format('DD/MM/YYYY')
    },
    getQRcode(){
      let opts = {
            errorCorrectionLevel: "L",//容错级别
            type: "image/png",//生成的二维码类型
            quality: 0.3,//二维码质量
            margin: 5,//二维码留白边距
            width: 128,//宽
            height: 128,//高
            text: "http://www.baidu.com",//二维码内容
            color: {
                dark: "#666666",//前景色
                light: "#fff"//背景色
            }
      }
      //this.QRlink 生成的二维码地址url
      QRCode.toDataURL(this.QRlink, opts , (err, url) => {
              if (err) throw err
              //将生成的二维码路径复制给data的QRImgUrl
              this.QRImgUrl= url
        })
      },
    // 数组转树
    toTree () {
      const data = [
        { pid: 1, id: 2, name: '一级' },
        { pid: 2, id: 3, name: '二级' },
        { pid: 3, id: 4, name: '三级' },
        { pid: 4, id: 5, name: '四级' },
        { pid: 4, id: 6, name: '五级' },
        { pid: 4, id: 7, name: '六级' }
      ]
      // 使用方法
      console.log(data)
      this.arrayToTree(data, { id: 'id', pid: 'pid' })
      console.log(data)
    },
    arrayToTree (array, paramsKey) {
      const pid = paramsKey.pid
      const id = paramsKey.id
      let copyArr = JSON.parse(JSON.stringify(array))
      array.forEach(function (item) {
        copyArr = copyArr.filter(function (child) {
          return child[pid] !== item[id]
        })
      })
      function treeLoop (arr = [], total = []) {
        for (let i = 0; i<arr.length; i++) {
          const aid = arr[i][id]
          let children = total.filter(function (child) {
            return child[pid] === aid
          })
          if (children.length > 0) {
            children = treeLoop(children, total)
          }
          arr[i].children = children
        }
        return arr
      }
      return treeLoop(copyArr, array)
    }
  }
}
</script>

<style lang="less" scoped>
.el-button {
  padding: 5px;
}
</style>
