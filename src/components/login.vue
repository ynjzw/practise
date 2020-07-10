<template>
  <div id="app">
    <layout>
      <Header :style="{background:'#5585c9',height:'100px'}">
        <div id="title" :style="{width:'400px'}">
          <img src="../images/smallClaimLogo.png" height="100px" width="400px">
        </div>

      </Header><br>
      <Layout>
        <div id="content">
          <form id="box">
            <formitem id="account" style="">
              <input v-model="userInfo.account">
              <span slot="prerend">
                <icon size="16px" type="person"></icon>
              </span>
            </formitem><br>
            <formitem>
              <input v-model="userInfo.passWd">
              <span slot="prerend">
                <icon size="16px" type="locked"></icon>
              </span>
            </formitem><br>
            <formitem id="role" style="margin-top: 20px">
              <label>角色：</label>
              <select v-model="userInfo.role" >
                <option value="" seleted disabled>请选择</option>
                <option v-for="item in roleList" :value="item.value" :key="item.value">{{item.label}}</option>
              </select>
            </formitem><br>
            <formitem id="test">
              <input placeholder="请输入验证码">
              <div id="changePic" @click="changePic">
                <identify :identifyCode="userInfo.identifyCode"></identify>
              </div>
            </formitem>
            <Button id="loginB" @click="login" type="primary" shape="circle">登录</Button><br>
            <div id="snap">
              <p>请使用chrome浏览器<a href="http://down10.zol.com.cn/ceshi/ChromeSetup.exe">下载</a></p>
              <div id="register">
                <p>没有账号?<a>立即注册</a></p>
                <modal id="registerPage">

                </modal>
              </div>
              <div id="findPw">
                <p>忘记密码?<a>找回密码</a></p>
                <modal id="findPwPage">

                </modal>
              </div>
            </div>
          </form>
          <div id="banner">
            <Carousel autoplay v-model="value2" loop>
              <CarouselItem>
                <img src="../images/banner1.png" width="100%" alt="banner">
              </CarouselItem>
              <CarouselItem>
                <img src="../images/banner2.png" width="100%" alt="banner">
              </CarouselItem>
              <CarouselItem>
                <img src="../images/banner3.png" width="100%" alt="banner">
              </CarouselItem>
            </Carousel>

          </div>
        </div><br>
      </Layout>
      <layout>
        <div id="footer">
          <p id="siter">厦门市湖里区人民法院</p>

          <div id="outsiteCont">
            <a href="http://218.5.2.1:18080/">法务云盘</a>
            <a href="http://courtapp.chinacourt.org/">最高人民法院</a>
            <a href="https://www.fjcourt.gov.cn/">福建省高级人民法院</a>
            <a href="https://www.xmcourt.gov.cn/">厦门市中级人民法院</a>
            <a href="http://tingshen.court.gov.cn/">中国庭审公开网</a>
          </div>
          <p id="suppoter">技术支持:厦门纵横集团</p>
        </div>

      </layout>
    </layout>
  </div>

</template>

<script>
  import Identify from "./identify";
  import home from "./home";
    export default {
        name: "login",
      components: {Identify},
      data(){
          return{
            userInfo:{
              account:'',
              passWd:'',
              role:'',
              identifyCode:'',
            },

            currentIndex:0,

            timer:null,
            bannerList:[
              "../images/banner1.jpg",
              "../images/banner2.jpg",
              "../images/banner3.jpg",
            ],
            roleList:[
              {
                label:'当事人',
                value:'当事人'
              },
              {
                label:'代理人',
                value:'代理人'
              }
            ]
          }
      },
      computed: {
          //上一张
          prePage(){
            if (this.currentIndex===0){
              return this.bannerList.length-1
            }
            else {
              return this.currentIndex-1
            }
        },
        //下一张
        nextPage(){
          if (this.currentIndex===this.bannerList.length-1){
            return 0
          }
          else {
            return this.currentIndex+1
          }
        }
      },
      methods:{
          login(){},
        changePic(){},
        click(){},
        //点击圆点切换图片
        gotoPage(index){
            this.currentIndex=index
        },
      }
    }
</script>

<style scoped>
@import "login.less";
</style>
