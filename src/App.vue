<template>
  <div id="app">
    <header>
      <nav class="navbar">
        <div class="container navbar-header">
          <!-- <a href="/" id="logo">Wind Mt</a> -->
        </div>
      </nav>
      <h1>赛事照片</h1>
      <p>仅供测试和学习交流，目前仅支持「i云动」</p>
      <div class="search-wraper">
        <el-input class="search" placeholder="请输入链接，例如http://m.yundong.runnerbar.com/m/7208387" icon="search" v-model="url" :on-icon-click="handleIconClick" @keyup.enter="handleIconClick">
        </el-input>
      </div>
    </header>

    <main class="main" v-show="hasResult">
      <div class="container">
        <div class="btns">
          <el-button-group>
            <el-button type="default" :class="[num == 1 ? 'el-button--success' : '']" v-on:click="handleBtnClick(1)">缩略图</el-button>
            <el-button type="default" :class="[num == 2 ? 'el-button--success' : '']" v-on:click="handleBtnClick(2)">高清图</el-button>
            <el-button type="default" :class="[num == 3 ? 'el-button--success' : '']" v-on:click="handleBtnClick(3)">超清图</el-button>
            <el-button type="default" :class="[num == 4 ? 'el-button--success' : '']" v-on:click="handleBtnClick(4)">原图</el-button>
          </el-button-group>
        </div>
        <div class="image"></div>
      </div>
    </main>

    <footer id="footer">
      <div class="instruction">
        <el-row :gutter="20">
          <el-col :span="12">
            <div class="grid-content">
              <h4>使用说明</h4>
              <p>
                <span>目前仅支持「i云动」这一个平台</span><br>
                <span>将「i云动」上
                  <strong>单张照片</strong>分享到微信或者其他工具上，用浏览器打开（在手机微信里边可以选择用 safari 或其他浏览器打开），然后直接把地址贴过来</span>
                <br>
                <span>如果在微信上，本网页可能会
                  <strong>被微信重新排版</strong>，导致看不到输入框。解决办法是点击右上角按钮，选择在浏览器中打开，然后点左上角的原网页打开即可</span>
              </p>
            </div>
          </el-col>
          <el-col :span="12">
            <div class="grid-content">
              <h4>免责声明</h4>
              <p>
                <span class="package-amount">本网站所有内容都是靠程序在互联网上自动搜集而来，仅供测试和学习交流。</span><br>
                <span class="package-amount">若侵犯了您的权益，请即时
                  <a href="mailto:&#122;&#121;&#98;&#115;&#116;&#97;&#114;&#116;&#64;&#113;&#113;&#46;&#99;&#111;&#109;" style="color: #f4f4f4;text-decoration: underline;">发邮件</a>通知站长万分感谢！</span>
              </p>
            </div>
          </el-col>
        </el-row>
      </div>
      <div class="copy-right">
        <span>© 2017</span>
        <a href="/">Wind Mt</a>
      </div>
    </footer>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      msg: 'Want something new?',
      url: '',
      hasResult: false,
      num: 1
    }
  },

  methods: {
    startHacking() {
      this.$notify({
        title: 'Shhh',
        message: 'Just be patient...',
        duration: 6000
      })
    },
    handleIconClick() {
      this.url = this.url.trim()
      if(this.url.length == 0){
        console.log("url is empty")
        return;
      }
      var url = "http://127.0.0.1:18088/tools/iyundong/images?url=" + this.url;
      var currentUrl = location.search;
      if (currentUrl.indexOf("?") != -1) {
        url = url + "&" + currentUrl.substr(1);
      }

      axios
        .get(url)
        .then(resp => console.log(resp.data))
        .catch(error => console.log(error))
      console.log(this.url);
    },
    handleBtnClick(n) {
      this.num = n
    }
  }
}
</script>

<style>
html,
body,
div {
  height: 100%
}

* {
  box-sizing: border-box;
}

body {
  background-color: #f5f5f5;
  margin: 0;
}

#app {
  font-family: Helvetica, sans-serif;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  min-height: 100%;
  position: relative;
}

h1 {
  font-size: 56px;
  text-shadow: -5px 5px 0 rgba(0, 0, 0, .1);
  margin-top: 20px;
  margin-bottom: 10px;
  line-height: 1.1;
  font-weight: 500;
}

a {
  text-decoration: none;
}

.navbar {
  min-height: 50px;
  padding-top: 20px;
}

#logo {
  background: url("https://ideassea.com/content/images/2017/07/logo-1.png");
  background-size: contain;
  background-repeat: no-repeat;
  width: 124px;
  height: 50px;
  font: 0/0;
  text-shadow: none;
  color: transparent;
  background-color: transparent;
  float: left;
}

header {
  color: #444;
  padding-right: 15px;
  padding-left: 15px;
}

header p {
  color: #888;
  margin-bottom: 15px;
  font-size: 21px;
  font-weight: 200;
  margin: 0 0 10px;
}

.search-wraper {
  max-width: 680px;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 10px;
}

.search input {
  font-size: 16px;
  padding: 13px 0px;
  border-radius: 0;
  height: auto;
  border-color: transparent;
  text-align: center;
  color: #000;
}

.search input:focus {
  -webkit-box-shadow: 0 0 6px rgba(0, 0, 0, .6);
  box-shadow: 0 0 6px rgba(0, 0, 0, .6);
  border-color: transparent;
}

.search input:hover {
  border-color: transparent;
}

h4 {
  margin-top: 10px;
  margin-bottom: 10px;
}

.el-button,
.el-button:active,
.el-button:focus,
.el-button:hover {
  border: none;
}

.main {
  padding-bottom: 50px;
  /* Height of the footer */
}

.instruction {
  display: none;
  padding: 20px 100px;
  text-align: start;
  color: #888;
}

.instruction p {
  font-size: 12px;
}

#footer {
  text-align: start;
  color: #444;
  position: absolute;
  bottom: 0;
  width: 100%;
}

#footer .copy-right {
  height: 50px;
  background-color: rgba(51, 51, 51, .08);
  line-height: 50px;
  text-align: center;
  font-weight: 100;
  font-size: 14px;
}

#footer .copy-right>*+* {
  margin-left: 14px;
}

#footer a {
  color: #444;
  border-bottom: dotted 1px #a9dfbf;
}

.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 15px;
  padding-right: 15px;
}

@media (min-width: 768px) {
  .container {
    width: 750px;
  }
}

@media (min-width: 992px) {
  .container {
    width: 970px;
  }
}

@media (min-width: 1200px) {
  .container {
    width: 1170px;
  }
}
</style>
