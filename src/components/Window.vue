/*
* MIT License
*
* Copyright (c) 2017 TechCatsLab
*
* Permission is hereby granted, free of charge, to any person obtaining a copy
* of this software and associated documentation files (the "Software"), to deal
* in the Software without restriction, including without limitation the rights
* to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
* copies of the Software, and to permit persons to whom the Software is
* furnished to do so, subject to the following conditions:
*
* The above copyright notice and this permission notice shall be included in all
* copies or substantial portions of the Software.
*
* THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
* IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
* FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
* AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
* LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
* OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
* SOFTWARE.
*/
/**
* Revision History:
*     Initial: 2017/07/19       Wang Bofeng
*/

<template xmlns="http://www.w3.org/1999/html" xmlns:v-drag="http://www.w3.org/1999/xhtml"
           xmlns="http://www.w3.org/1999/html">
  <div id="Window">
    <img id="Background" v-on:click="menuVisible" src="../img/background.jpeg"/>
    <router-view></router-view>
    <div id="Footer" v-if="footerVisible">
      <div id="Start" v-on:click="showWindow">
        <img src="../img/start.png"  style="float: left">
      </div>
      <div id="Time"></div>
      <div id="Date"></div>
    </div>
    <file-manager v-show="showFile" @showFilemanager="showFilemanager" ></file-manager>
    <notebook v-show="showNote"></notebook>
    <transition name="el-fade-in-linear">
      <div id="WindowsMenu" v-show="seen" >
      <div id="Menu" >
        <div id="User">
          <img  id="Userlogo" src="../img/user_logo.png" />
          <div id="Username">Yan Tsishko</div>
        </div>
        <div id="Life">
          <div id="Lifetitle">Life at a glance</div>
          <div id="Lifecontent">
            <el-row :gutter="5">
              <el-col :span="8">
                <div class="grid-content border text" id="Calendar" v-on:click="showCalendar('Calendar_content')">
                  <span class="content-title">Calendar</span>
                </div>
              </el-col>
              <el-col :span="16">
                <div class="grid-content border text" id="Email" v-on:click="showEmail('Email_content')">
                  <span class="content-title">E-mail</span>
                </div>
              </el-col>
            </el-row>
            <el-row :gutter="5">
              <el-col :span="16">
                <div class="grid-content border text" id="Photos" v-on:click="showPhotos('Photos_content')">
                  <span class="content-title">Photos</span>
                </div>
              </el-col>
              <el-col :span="8">
                <div class="grid-content border text" id="Friend" v-on:click="showFriend('Friend_content')">
                  <span class="content-title">Friend</span>
                </div>
              </el-col>
            </el-row>
            <el-row :gutter="5">
              <el-col :span="8">
                <div class="grid-content border text" id="Install" v-on:click="showInstall('Install_content')">
                  <span class="content-title">Install</span>
                </div>
              </el-col>
              <el-col :span="16">
                <div class="grid-content border text" id="Video" v-on:click="showVideo('Video_content')">
                  <span class="content-title">Video</span>
                </div>
              </el-col>
            </el-row>
          </div>
        </div>
        <div id="Play">
          <div id="Playtitle">Play and Explore</div>
          <div id="Playcontent">
          <el-row :gutter="5">
            <el-col :span="8">
              <div class="grid-content border text" id="Game" v-on:click="showGame('Game_content')">
                <span class="content-title">Game</span>
              </div>
            </el-col>
            <el-col :span="8">
              <div class="grid-content border text" id="Music" v-on:click="showMusic('Music_content')">
                <span class="content-title">Music</span>
              </div>
            </el-col>
            <el-col :span="8">
              <div class="grid-content border text" id="Camera" v-on:click="showCamera('Camera_content')">
                <span class="content-title">Camera</span>
              </div>
            </el-col>
          </el-row>
          <el-row :gutter="5">
            <el-col :span="8">
              <div class="grid-content border text" id="Sports" v-on:click="showSports('Sports_content')">
                <span class="content-title">Sports</span>
              </div>
            </el-col>
            <el-col :span="16">
              <div class="grid-content border text" id="News" v-on:click="showNews('News_content')">
                <span class="content-title">News</span>
              </div>
            </el-col>
          </el-row>
          <el-row :gutter="5">
            <el-col :span="8">
              <div class="grid-content border text" id="Store" v-on:click="showStore('Store_content')">
                <span class="content-title">Store</span>
              </div>
            </el-col>
            <el-col :span="8">
              <div class="grid-content border text" id="Money" v-on:click="showMoney('Money_content')">
                <span class="content-title">Money</span>
              </div>
            </el-col>
            <el-col :span="8">
              <div class="grid-content border text" id="Travel" v-on:click="showTravel('Travel_content')">
                <span class="content-title">Travel</span>
              </div>
            </el-col>
          </el-row>
          </div>
        </div>
        <div id="Mostused">
          <span id="Mostuesdtitle">Most used</span>
        </div>
        <el-button type="text" @click="signOut" id="SignOut">
          <img src="../img/signout.png"/>
          <span class="buttonText">sign out</span>
        </el-button>
      </div>
      </div>
    </transition>
    <div id="Calendarcontent" class="content" v-show="seen_calendar" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeCalendar">
          <img class="close-png" src="../img/close_button.png" />
        </div>
        <div class="name">Calendar</div>
      </div>
      <img class="content-body" id="content" src="../img/calendar.png" />
    </div>
    <div id="Emailcontent" class="content" v-show="seen_email" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeEmail">
          <img class="close-png" src="../img/close_button.png" />
        </div>
        <div class="name">Email</div>
      </div>
      <img class="content-body" src="../img/20.png" />
    </div>
    <div id="Photoscontent" class="content" v-show="seen_photos" v-drag>
      <div class="title">
        <div class="close" v-on:click="closePhotos">
          <img class="close-png" src="../img/close_button.png" />
        </div>
        <div class="name">Photos</div>
        <img class="content-body" src="../img/shop.png"/>
      </div>
    </div>
    <div id="Friendcontent" class="content" v-show="seen_friend" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeFriend">
          <img class="close-png" src="../img/close_button.png"/>
        </div>
        <div class="name">Friend</div>
      </div>
      <img class="content-body" src="../img/34.png"/>
    </div>
    <div id="Installcontent" class="content" v-show="seen_install" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeInstall">
          <img class="close-png" src="../img/close_button.png"/>
        </div>
        <div class="name">Install</div>
      </div>
      <img class="content-body" src="../img/06.png"/>
    </div>
    <div id="Videocontent" class="content" v-show="seen_video" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeVideo">
          <img class="close-png" src="../img/close_button.png"/>
        </div>
        <div class="name">Video/div>
        </div>
        <img class="content-body" src="../img/video.png"/>
      </div>
    </div>
    <div id="Gamecontent" class="content" v-show="seen_game" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeGame">
          <img class="close-png" src="../img/close_button.png"/>
        </div>
        <div class="name">Games/div>
        </div>
        <img class="content-body" src="../img/games.png"/>
      </div>
    </div>
    <div id="Musiccontent" class="content" v-show="seen_music" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeMusic">
          <img class="close-png" src="../img/close_button.png"/>
        </div>
        <div class="name">Music</div>
        </div>
      <img class="content-body" src="../img/music.png"/>
    </div>
    <div id="Cameracontent" class="content" v-show="seen_camera" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeCamera">
          <img class="close-png" src="../img/close_button.png"/>
        </div>
        <div class="name">Camera</div>
        <img class="content-body" src="../img/camera.png"/>
      </div>
    </div>
    <div id="Sportscontent" class="content" v-show="seen_sports" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeSports">
          <img class="close-png" src="../img/close_button.png" />
        </div>
        <div class="name">Sports</div>
        <img class="content-body" src="../img/shop.png"/>
      </div>
    </div>
    <div id="Newscontent" class="content" v-show="seen_news" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeNews">
          <img class="close-png" src="../img/close_button.png" />
        </div>
        <div class="name">News</div>
        <img class="content-body" src="../img/shop.png"/>
      </div>
    </div>
    <div id="Storecontent" class="content" v-show="seen_store" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeStore">
          <img class="close-png" src="../img/close_button.png"/>
        </div>
        <div class="name">Store</div>
        <img class="content-body" src="../img/shop.png"/>
      </div>
    </div>
    <div id="Moneycontent" class="content" v-show="seen_money" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeMoney">
          <img class="close-png" src="../img/close_button.png"/>
        </div>
        <div class="name">Money</div>
      </div>
        <img class="content-body" src="../img/graph.png"/>
    </div>
    <div id="Travelcontent" class="content" v-show="seen_travel" v-drag>
      <div class="title">
        <div class="close" v-on:click="closeTravel">
          <img class="close-png" src="../img/close_button.png"/>
        </div>
        <div class="name">Travel</div>
        <img class="content-body" src="../img/24.png"/>
      </div>
    </div>
    <div id="Signin" v-if="signinVisible">
      <img id="UserLogo" src="../img/user_logo.png"/>
      <span id="UserName">Yan Tsishko</span>
      <el-button type="success" id="SigninButton" v-on:click="signIn">Sign In</el-button>
    </div>
  </div>
</template>

<script>
  import fileManager from './Filemanager.vue'
  import ElButton from '../../node_modules/element-ui/packages/button/src/button.vue'
  import Notebook from './Notebook.vue'
  import ElDialog from '../../node_modules/element-ui/packages/dialog/src/component.vue'
  function setTime () {
    document.getElementById('Time').innerHTML = 0
    var time = new Date()
    var hour = time.getHours()
    if (hour <= 9) { hour = '0' + hour }
    var minute = time.getMinutes()
    if (minute <= 9) { minute = '0' + minute }
    var second = time.getSeconds()
    if (second <= 9) { second = '0' + second }
    var times = hour + ':' + minute + ':' + second
    document.getElementById('Time').innerHTML = times
  }
  setInterval(setTime, 1000)
  function setDate () {
    document.getElementById('Date').innerHTML = 0
    var date = new Date().toLocaleDateString()
    document.getElementById('Date').innerHTML = date
  }
  setInterval(setDate, 1000)
  export default{
    data () {
      return {
        seen: false,
        seen_calendar: false,
        seen_email: false,
        seen_photos: false,
        seen_friend: false,
        seen_install: false,
        seen_video: false,
        seen_game: false,
        seen_music: false,
        seen_camera: false,
        seen_sports: false,
        seen_news: false,
        seen_store: false,
        seen_money: false,
        seen_travel: false,
        footerVisible: true,
        signinVisible: false,
        Zindex: 10,
        showFile: true,
        showNote: true
      }
    },
    components: {
      ElDialog,
      ElButton,
      fileManager,
      Notebook
    },
    methods: {
      showWindow () {
        this.seen = !this.seen
      },
      showCalendar (id) {
        this.seen_calendar = true
        this.seen = !this.seen
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeCalendar () {
        this.seen_calendar = false
      },
      showEmail (id) {
        this.seen = !this.seen
        this.seen_email = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeEmail () {
        this.seen_email = false
      },
      showPhotos (id) {
        this.seen = !this.seen
        this.seen_photos = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closePhotos () {
        this.seen_photos = false
      },
      showFriend (id) {
        this.seen = !this.seen
        this.seen_friend = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeFriend () {
        this.seen_friend = false
      },
      showInstall (id) {
        this.seen = !this.seen
        this.seen_install = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeInstall () {
        this.seen_install = false
      },
      showVideo (id) {
        this.seen = !this.seen
        this.seen_video = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeVideo () {
        this.seen_video = false
      },
      showGame (id) {
        this.seen = !this.seen
        this.seen_game = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeGame () {
        this.seen_game = false
      },
      showMusic (id) {
        this.seen = !this.seen
        this.seen_music = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeMusic () {
        this.seen_music = false
      },
      showCamera (id) {
        this.seen = !this.seen
        this.seen_camera = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeCamera () {
        this.seen_camera = false
      },
      showSports (id) {
        this.seen = !this.seen
        this.seen_sports = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeSports () {
        this.seen_sports = false
      },
      showNews (id) {
        this.seen = !this.seen
        this.seen_news = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeNews () {
        this.seen_news = false
      },
      showStore (id) {
        this.seen = !this.seen
        this.seen_store = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeStore () {
        this.seen_store = false
      },
      showMoney (id) {
        this.seen = !this.seen
        this.seen_money = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeMoney () {
        this.seen_money = false
      },
      showTravel (id) {
        this.seen = !this.seen
        this.seen_travel = true
        this.Zindex = this.Zindex + 1
        document.getElementById(id).style.zIndex = this.Zindex
      },
      closeTravel () {
        this.seen_travel = false
      },
      signOut () {
        this.footerVisible = false
        this.dhtmlVisible = false
        this.fileVisible = false
        this.dtmlVisible = false
        this.seen = false
        this.signinVisible = true
        this.showFile = false
        this.showNote = false
      },
      signIn () {
        this.footerVisible = true
        this.dhtmlVisible = true
        this.fileVisible = true
        this.dtmlVisible = true
        this.signinVisible = false
        this.showFile = true
        this.showNote = true
      },
      showFilemanager () {
        this.seen = !this.seen
      },
      menuVisible () {
        if (this.seen === true) {
          this.seen = false
        }
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  *{
    margin: 0;
    padding: 0;
  }

  body{
    overflow: hidden;
    min-width: 1520px;
    min-height: 1440px;
    -ms-user-select: none;
    -moz-user-select: none;
    user-select: none;
  }

  #Background{
    width: 1920px;
    height: 1080px;
    position: absolute;
    left: 0px;
    top: 0px;
  }

  #Footer{
    width: 100%;
    background-color: black;
    opacity: 0.85;
    position: absolute;
    bottom: 0;
    z-index: 1000;
  }

  #Start{
    width: 50px;
  }

  #Start:hover{
    opacity: 0.6;
  }

  #Time{
    color: white;
    font-size: 15px;
    position: absolute;
    right: 14px;
    top: 2px;
  }

  #Date{
    color: white;
    font-size: 15px;
    position: absolute;
    bottom: 0;
    right: 13px;
  }

  #Menu{
    background-color: rgba(0,0,0,.8);
    width:850px;
    height: 380px;
    position: absolute;
    bottom: 41px;
    z-index: 400;
  }

  #Userlogo{
    border-radius: 50px;
    float: left;
    margin-left: 10px;
    margin-top: 10px;
  }

  #Username{
    color: white;
    float: left;
    margin-top: 25px;
    margin-left: 5px;
  }

  #Mostused{
    position: absolute;
    top: 80px;
    left: 20px;
    width: 150px;
    height: 200px;
  }

  #Mostuesdtitle{
    color: #8c939d;
  }

  #SignOut{
    position: absolute;
    top: 330px;
    left: 20px;
  }

  .buttonText{
    font-size: 16px;
    color: white;
    position: absolute;
    left: 20px;
  }

  #Life{
    position: relative;
    height: 300px;
    width: 300px;
    margin-left: 210px;
    margin-top: 20px;
  }

  #Lifecontent{
    width: 310px;
    height: 280px;
    position: absolute;
    margin-top: 30px;
  }

  .el-row {
     margin-bottom: 5px;
  }

  .bg-purple {
    background: #d3dce6;
  }

  .grid-content {
    border-radius: 1px;
    min-height: 90px;
    min-width: 90px;
  }

  .row-bg {
    padding: 5px 5px;
    background-color: #f9fafc;
  }

  #Lifetitle{
    margin-left: 0;
    position: absolute;
    margin-top: 5px;
    color: white;
  }

  .content-title{
    position: absolute;
    bottom: 3px;
  }

  #Calendar{
    background: #107c10;
    background-image : url("../img/calendar.png");
    background-repeat: no-repeat;
    background-size: 55% 55%;
    background-position: center center;
    position: relative;
  }

  #Email{
    background-color: #00b1f0;
    background-image: url("../img/20.png");
    background-repeat: no-repeat;
    background-size: 32% 58%;
    background-position: center center;
    position: relative;
  }

  #Photos{
    background-image: url("../img/photos.png");
    background-repeat: no-repeat;
    background-position: center center;
    position: relative;
  }

  #Friend{
    background-image: url("../img/34.png");
    background-repeat: no-repeat;
    background-size: 65% 65%;
    background-position: center center;
    background-color: #00b1f0;
    position: relative;
  }

  .text{
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
    font-size: 14px;
    color: white;
  }

  #Install{
    background-color: #2143af;
    background-repeat: no-repeat;
    background-size: 50% 50%;
    background-position: center center;
    background-image: url("../img/06.png");
    position: relative;
  }

  #Video{
    background-repeat: no-repeat;
    background-size: 35% 60%;
    background-position: center center;
    background-color: #90228a;
    background-image: url("../img/31.png");
    position: relative;
  }

  #Play{
    position: relative;
    height: 300px;
    width: 300px;
    margin-left: 530px;
    margin-top: -300px;
  }

  #Playcontent{
    width: 310px;
    height: 280px;
    position: absolute;
    margin-top: 30px;
  }

  #Playtitle{
    margin-left: 0;
    position: absolute;
    margin-top: 5px;
    color: white;
  }

  #Game{
    background: #2143af;
    background-repeat: no-repeat;
    background-size: 50% 50%;
    background-position: center center;
    background-image: url("../img/games.png");
    position: relative;
  }

  #Music{
    background-repeat: no-repeat;
    background-size: 50% 50%;
    background-position: center center;
    background-color: #e12429;
    background-image: url("../img/music.png");
    position: relative;
  }

  #Camera{
    background-repeat: no-repeat;
    background-size: 50% 50%;
    background-position: center center;
    background-color: #90228a;
    background-image: url("../img/camera.png");
    position: relative;
  }

  #Sports{
    background-repeat: no-repeat;
    background-position: center center;
    background-image: url("../img/sports.png");
    position: relative;
  }

  #News{
    background-repeat: no-repeat;
    background-position: center center;
    background-image: url("../img/news.png");
    position: relative;
  }

  #Store{
    background-repeat: no-repeat;
    background-size: 50% 50%;
    background-position: center center;
    background-color: #107c10;
    background-image: url("../img/shop.png");
    position: relative;
  }

  #Money{
    background-repeat: no-repeat;
    background-size: 50% 50%;
    background-position: center center;
    background-image: url("../img/graph.png");
    background-color: #2143af;
    position: relative;
  }

  #Travel{
    background-repeat: no-repeat;
    background-size: 50% 50%;
    background-position: center center;
    background-color: #00b1f0;
    background-image: url("../img/24.png");
    position: relative;
  }

  .title{
    height: 25px;
    width: 100%;
    background-color: white;
    position: absolute;
  }

  .name{
    font-size: 12px;
    position: absolute;
    margin-left: 15px;
    margin-top: 5px;
  }

  .close{
    width: 25px;
    height: 25px;
    position: absolute;
    margin-left: 726px;
  }

  .close-png{
    width: 10px;
    height: 10px;
    position: absolute;
    margin-top: 7.5px;
    margin-left: -5px;
  }

  .content-body{
    margin-top: 150px;
    margin-left: -50px;
  }

  .close:hover{
    background-color: red;
  }

  .border:hover{
    box-shadow: inset 0px 0px 2px 2px rgba(255,255,255,0.8);
  }

  #Calendarcontent{
    width: 750px;
    height: 450px;
    left: 400px;
    top: 100px;
    position: absolute;
    background-color: #107c10;
  }

  #Emailcontent{
    width: 750px;
    height: 450px;
    position: absolute;
    background-color: #00b1f0;
  }

  #Photoscontent{
    width: 750px;
    height: 450px;
    position: absolute;
    background-color: #00b1f0;
  }

  #Friendcontent{
    width: 750px;
    height: 450px;
    position: absolute;
    background-color: #00b1f0;
  }

  #Installcontent{
    width: 750px;
    height: 450px;
    position: absolute;
    background-color: #2143af ;
  }

  #Videocontent{
    background-color: #90228a;
    width: 750px;
    height: 450px;
    position: absolute;
  }

  #Gamecontent{
    width: 750px;
    height: 450px;
    position:absolute;
    background-color: #2143af ;
  }

  #Musiccontent{
     width: 750px;
     height: 450px;
     position: absolute;
     background-color: #e12429 ;
   }

  #Cameracontent{
    width: 750px;
    height: 450px;
    position: absolute;
    background-color: #90228a;
  }

  #Sportscontent{
    width: 750px;
    height: 450px;
    position:absolute;
    background-color: #00b1f0;
  }

  #Newscontent{
    width: 750px;
    height: 450px;
    position: absolute;
    background-color: #00b1f0;
  }

  #Storecontent{
    width: 750px;
    height: 450px;
    position: absolute;
    background-color: #107c10;
  }

  #Moneycontent{
    width: 750px;
    height: 450px;
    position: absolute;
    background-color: #2143af;
  }

  #Travelcontent{
    width: 750px;
    height: 450px;
    position: absolute;
    background-color: #00b1f0;
  }

  .content{
    position: absolute;
    top: 100px;
    left: 400px;
    text-align: center;
  }

  #UserLogo{
    border-radius: 100px;
    width: 70px;
    height: 70px;
    position: absolute;
    top: 250px;
    left: 750px;
  }

  #UserName{
    position: absolute;
    top: 340px;
    left: 735px;
    color: white;
    font-size: 20px;
  }

  #SigninButton{
    position: absolute;
    top: 390px;
    left: 750px;
  }
</style>
