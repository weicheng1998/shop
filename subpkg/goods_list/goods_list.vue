<template>
  <view>
   <view class="goods-list">
    <view v-for="(goods,i) in goodsList" :key="i" @click="gotoDetail(goods)">
      <my-goods :goods="goods"></my-goods>
   </view>
  </view>
   </view>
</template>

<script>
  export default {
    data() {
      return {
        queryObject:{
          query:'',
          cid:'',
          pagenum:1,
          pagesize:10
        },
        goodsList:[],
        total:0,
       isloading:false
      };
    },
    onLoad(options){
      this.queryObject.query=options.query||''
      this.queryObject.cid=options.cid||''
      this.getGoodsList()
    },
    methods:{
     async getGoodsList(cb){
       this.isloading=true;
      const {data:res}= await uni.$http.get('/api/public/v1/goods/search',this.queryObject)
      this.isloading=false
      cb&&cb()
      if(res.meta.status!==200) return uni.$showMsg()
      this.goodsList=[...this.goodsList,...res.message.goods]
      this.total=res.message.total
      },
      gotoDetail(goods){
        uni.navigateTo({
          url:'/subpkg/goods_detail/goods_detail?goods_id='+goods.goods_id
        })
      }
    },
    onReachBottom() {
      if(this.queryObject.pagenum * this.queryObject.pagesize>=this.total) return uni.$showMsg('数据加载完毕')
      if (this.isloading) return
      this.queryObject.pagenum++
      this.getGoodsList()
    },
    onPullDownRefresh(){
      this.queryObject.pagenum=1
      this.total=0
      this.isloading=false
      this.goodsList=[]
      this.getGoodsList(()=>uni.stopPullDownRefresh())
    }
  }
</script>

<style lang="scss">

</style>
