---
title: 非插件实现幻灯片效果
date: 2018-01-11 14:48:43
tags:
---
很多网站都有幻灯片效果需求，我们大多时候会采用插件形式，其实这个不难，下面是手写幻灯片效果的部分代码。
<!-- more -->
###### html代码
```html
<div class="block-slides">
    <div class="slider-component">
        <ul class="slide-list">
            <li class="slide-item" style="background-color: #2d233c; background-image: url(/assets/img/slides/financing.jpg);">
                <div class="layout">
                    <div class="left">
                        <p class="title">安畅网络完成B轮融资</p>
                        <p class="text">全面加速云集成战略，并启用新品牌标志</p>
                        <a class="btn-blank btn" href="{{env('WEB_PROD_URL')}}/news/5128">了解详情</a>
                    </div>
                </div>
            </li>
            <li class="slide-item" style="background-color: #2d233c; background-image: url(/assets/img/slides/smartguard.jpg);">
                <div class="layout">
                    <div class="left">
                        <p class="title">SmartGuard高等级安全防护平台</p>
                        <p class="text">集中安全管控IT资源，7X24守护业务系统</p>
                        <a class="btn-blank btn" href="{{route('smartguard')}}">了解详情</a>
                    </div>
                </div>
            </li>
        </ul>
    </div>       
</div>
```
###### css代码
```css
.slider-component {
  position: relative;
  height: 550px;
  min-width: 1100px;
  overflow: hidden;
  background-color: #000000;
  .slide-list {
    position: relative;
    overflow: hidden;
    .slide-item {
      display: none;
      float: left;
      width: 100%;
      height: 550px;
      min-width: 1100px;
      background-position: center top;
      background-repeat: no-repeat;
      &.type-text {
        h3 {
          position: absolute;
          top: 74px;
          left: 0;
          line-height: 33px;
          font-size: 24px;
          color: #FFF;
        }
        .text {
          position: absolute;
          top: 126px;
          left: 0;
          line-height: 20px;
          font-size: 14px;
          color: #9BA3AF;
        }
      }
      &.active {
        display: block;
        .left {
          display: block;
        }
        .right {
          display: block;
        }
      }
      .left {
        width: 76%;
        position: absolute;
        left: 200px;
        margin:180px 0px 0px 0px;
        color: #fff;
        display: none;
        font-weight: lighter;
        .title {
          font-size: 44px;
          margin-bottom: 30px;
        }
        .text {
          font-size: 20px;
          letter-spacing: 3px;
        }
        .btn {
          display: inline-block;
          width: 148px;
          height: 48px;
          line-height: 48px;
          text-align: center;
          font-size: 18px;
          margin-top: 60px;
          border :1px solid #fff;
          border-radius: 4px;
          color: #fff;
          &:hover {
            border: 1px solid #E2003B;
          }
        }
      }
      .right {
        position: absolute;
        right: 200px;
        display: none;
        img {
          margin-top: 120px;
        }
      }
    }
  }
  .slide-control {
    .control-btn {
      position: absolute;
      top: 50%;
      width: 42px;
      height: 42px;
      margin-top: -21px;
      @include main-icons();
      cursor: pointer;
      &.prev-btn {
        left: 50px;
        background-position: 0 -198px;
        &:hover {
          background-position: -88px -198px;
        }
      }
      &.next-btn {
        right: 50px;
        background-position: -44px -198px;
        &:hover {
          background-position: -132px -198px;
        }
      }
    }
  }
  .show-icon {
    position: absolute;
    left: 50%;
    bottom: 30px;
    li.control-icon {
      display: block;
      float: left;
      width: 8px;
      height: 8px;
      bottom: 30px;
      border-radius: 50%;
      border: 1px solid #fff;
      margin-right: 10px;
      &.active {
        background-color: #ffffff;
      }
      &:hover {
        cursor: pointer;
      }
    }
  }
}
```
###### js代码
```js
  class Slider {
    constructor (options = {}) {
      this.options = {
        intervalTime: 5000,
        contentMove: '200px',
        contentMoveSpeed: 800,
        fadeInSpeed: 600,
        fadeOutSpeed: 500,
        ...options
      }
      this.stop = false
      this.index = 0
      this.num_index = 0
      this.controller = null
      this.init()
    }

    init () {
      let _this = this
      let $el = this.options.el
      let $li = $el.find('.slide-item')
      let slidesNum = $li.length
      let controlClass = 'slide-control dis-none'
      let showIconClass = 'show-icon'
      let $control = $('<div>').addClass(controlClass)
      let $showIcon = $('<ul>').addClass(showIconClass)

      // 控制按钮以及显示圆点
      if (slidesNum) {
        ['prev', 'next'].forEach((dest) => {
          let $btn = $('<div>').addClass(`control-btn ${dest}-btn`)
          $control.append($btn)
        })
        $('.slide-item').each(function(key){
          let $icon = $('<li>').addClass(`control-icon show-icon-${key}`)
          $showIcon.append($icon)
        })
      }
      $el.append($control)
      $el.append($showIcon)
      _this.indexChange()
      // 滑入容器
      $('.slider-component').mouseenter(()=>{
        $('.slide-control').removeClass('dis-none')
        this.stop = true
      })
      // 滑出容器
      $('.slider-component').mouseleave(()=>{
        $('.slide-control').addClass('dis-none')
        this.go()
      })
      // 点击左边控制器
      $('.slide-control .prev-btn').click(()=>{
        this.action('prev')
      })

      // 点击右边控制器
      $('.slide-control .next-btn').click(()=> {
        this.action('next')
      })

      // 点击num控制器
      $('.show-icon li').click(function() {
        _this.num_index = $(this).index();
        _this.action('num')
      })

      // 循环播放
      setInterval(()=>{
        if(this.stop) return;
        this.index++
        if (this.index == $li.length){
          this.index = 0;
        }
        _this.indexChange()
      },this.options.intervalTime)
    }
    // 超时后开始循环播放
    openAutoScroll () {
      this.controller = setTimeout(()=>{
        this.stop = false
      },this.options.intervalTime)
    }

    clearInterval () {
      clearTimeout(this.controller)
    }
    //手动跳转
    go () {
      this.clearInterval()
      this.action()
      this.openAutoScroll();
    }

    action (dest = 'next') {
      let $el = this.options.el
      let $li = $el.find('.slide-item')
      this.stop = true
      this.index = $el.find('.active').index()
      switch (dest) {
        case 'prev':
          this.index = this.index == 0 ? $li.last().index() : this.index - 1
          break;
        case 'next':
          this.index = this.index == $li.last().index() ? 0 : this.index + 1
          break;
        case 'num':
          this.index = this.num_index
          break;
        default:
          break;
      }
      this.indexChange(dest)
    }
    //样式变化
    indexChange () {
      let $el = this.options.el
      let $li = $el.find('.slide-item')
      let _this = this

      $('.show-icon li')
        .eq(this.index).addClass('active')
        .siblings('li').removeClass('active')

      $li
        .find('.left').css({'left': this.options.contentMove})

      $li
        .eq(this.index).animate({'opacity': 1},_this.options.fadeInSpeed).addClass('active')
        .siblings().animate({'opacity': 0},_this.options.fadeOutSpeed).removeClass('active')

      $li
        .eq(this.index).find('.left').animate({'left': 0},_this.options.contentMoveSpeed)
    }
  }
  module.exports = Slider

```
###### 调用方法
```js
    let options = {
      el: $('.block-slides-copy .slider-component')
    }
    let sliderCopy = new SliderCopy(options)
```
