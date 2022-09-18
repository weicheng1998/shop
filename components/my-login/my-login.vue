<template>
  <view>
   <view class="login-container">
     <uni-icons type="contact-filled" size="100" color="#afafaf"></uni-icons>
     <button type="primary" class="btn-login" @click="getUserProfile">一键登录</button>
     <text class="tips-text">登录后</text>
   </view>
  </view>
</template>

<script>
  import {mapMutations} from 'vuex'
  export default {
    name:"my-login",
    data() {
      return {
        
      };
    },
    methods:{
      ...mapMutations('m_user',['updateUserInfo','updateToken']),
       getUserProfile() {
             uni.getUserProfile({
               desc: '你的授权信息',
               success: (res) => {
                 // 将信息存到 vuex 中
                 this.updateUserInfo(res.userInfo)
                 this.getToken(res)
               },
               fail: (res) => {
                 return uni.$showMsg('您取消了登录授权')
               }
             })
    },
    getToken(info){ this.updateToken('token')  }
   // async getToken(info){
   //    const [err,res]=await uni.login().catch(err=>err)
   //    if(err||res.errMsg!=='login:ok') return uni.$showMsg('登陆失败')
   //    const query={
   //      code:res.code,
   //      encryptedData:info.encryptedData,
   //      iv:info.iv,
   //      signature:info.signature
   //    }
   //   const{data:loginResult}=await uni.$http.post('/api.public/v1/users/wxlogin',query)
   //   if(loginResult.meta.status!==200) return uni.$showMsg('登陆失败！')
   //   uni.$showMsg('登陆成功')
   //  }
  }}
</script>

<style lang="scss">
.login-container{
  height: 750rpx;
  background-color: #f8f8f8;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
  overflow: hidden;
  &::after{
    background-color: white;
    content:'';
    display: block;
    width: 100%;
    height: 40px;
    position: absolute;
    bottom: 0;
    left: 0;
    border-radius: 100%;
    transform: translateY(50%);
  }
  .btn-login{
width: 90%;
border-radius: 100px;
margin: 15px 0;
background-color: #c00000;
  }
  .tips-text{    
    font-size: 12px;
    color: gray;}
}
</style>