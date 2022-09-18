<template>
  <view class="my-search-container" :style="{'background-color':bgcolor}" @click="searchBoxHandler">
    <view class="my-search-box" :style="{'border-radius':radius+'px'}">
      <icon type="search" size="17"></icon>
      <text class="placeholder">搜索</text>
    </view>
  </view>
</template>

<script>
  export default {
    name:"my-search",
    props:{
      bgcolor:{
      type:String,
      default:'#C00000'
      },
      radius:{
        type:Number,
      default:18
      }
    },
    methods:{
      searchBoxHandler(){
        this.$emit('click')
      }
    },
    data() {
      return {
        
      };
    }
  }
</script>

<style lang="scss">
.my-search-container{
  height: 50px;
  // background-color: #c00000;
  display: flex;
  align-items: center;
  padding: 0 10px;
  .my-search-box{
    height: 36px;
    background-color: #ffffff;
    // border-radius: 18px;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    .placeholder{
      font-size: 15px;
      margin-left: 5px;
    }
  }
}
</style>