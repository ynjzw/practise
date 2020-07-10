<template>
  <div id="app">
    <layout>
      <Header :style="{background:'#5585c9',height:'100px'}">
        <div id="title" :style="{width:'400px'}">
          <img src="../images/smallClaimLogo.png" height="100px" width="400px">
        </div>

      </Header>
      <br>
      <Layout>
        <div id="content">
          <Form id="box" >
            <Formitem id="account" style="" prop="account" >
              <Input :style="{width:'100px',marginLeft:'10px'}"  v-model="userInfo.account" placeholder="请输入账号" @keyup.enter.native="login">
                <span slot="prepend">
                <Icon :size="20" type="person"></Icon>
              </span>
              </Input>
            </Formitem>

            <Formitem prop="passWd" >
              <Input v-model="userInfo.passWd" placeholder="请输入密码" @keyup.enter.native="login"><br>
                <span slot="prepend">
                <Icon :size="14" type="locked"></Icon>
              </span>
              </Input>
            </Formitem>

            <Formitem id="role" style="margin-top: 20px">
              <label>角色：</label>
              <Select v-model="userInfo.role">
                <option value="" seleted disabled>请选择</option>
                <option v-for="item in roleList" :value="item.value" :key="item.value">{{item.label}}</option>
              </Select>
            </Formitem>
            <br>
            <Formitem id="test">
              <Input placeholder="请输入验证码" v-model="userInfo.verifyCode"></Input>
              <div id="changePic" @click="changePic">
                <identify :identifyCode="identifyCode"></identify>
              </div>
            </Formitem>
            <br>
            <Button id="loginB" @click="login" type="primary" shape="circle">登录</Button>
            <br>
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
          </Form>
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
        </div>
        <br>
      </Layout>
      <layout>
        <div id="footer">
          <div id="outsiteCont">
            <a href="http://218.5.2.1:18080/">法务云盘</a>
            <a href="http://courtapp.chinacourt.org/">最高人民法院</a>
            <a href="https://www.fjcourt.gov.cn/">福建省高级人民法院</a>
            <a href="https://www.xmcourt.gov.cn/">厦门市中级人民法院</a>
            <a href="http://tingshen.court.gov.cn/">中国庭审公开网</a>
          </div>
          <p id="siter">厦门市湖里区人民法院</p>
          <p id="suppoter">技术支持:厦门纵横集团</p>
        </div>

      </layout>
    </layout>
  </div>

</template>

<script>
  import Identify from "./identify";//Identify为验证码插件
  import home from "./home";        //home是登录成功的跳转页面
  export default {
    name: "login",
    components: {Identify},
    data() {
      return {
        //登录用户信息
        userInfo: {
          account: '',
          passWd: '',
          role: '',
          verifyCode: '',
        },
        //输入的验证码
        identifyCodes: '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ',
        identifyCode:'',
        bannerList: [
          "../images/banner1.jpg",
          "../images/banner2.jpg",
          "../images/banner3.jpg",
        ],
        roleList: [
          {
            label: '当事人',
            value: '当事人'
          },
          {
            label: '代理人',
            value: '代理人'
          }
        ]
      }
    },
    mounted() {
      this.identifyCode=''
      this.makeCode(this.identifyCode,4)
    },
    computed: {
    },
    methods: {
      //登录验证及成功跳转
      login() {
      },
      //生成随机数
      randomNum(){
        return Math.floor(Math.random()*33)
      },
      //生成验证码
      makeCode(o,l){
        for (let i=0;i<l;i++){
          this.identifyCode+=this.identifyCodes[this.randomNum()]
        }
        console.log(this.identifyCode)
      },
      //更新验证码
      changePic() {
        this.identifyCode=''
        this.makeCode(this.identifyCode,4)
      },
      click() {
      },
    }
  }
</script>

<style scoped>
  @import "login.less";
</style>
