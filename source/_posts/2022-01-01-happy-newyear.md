---
title: 纯Js实现的烟花特效
top: false
cover: false
toc: false
mathjax: true
date: 2021-12-06 13:22:32
password:
summary:
tags:
- 特效
categories:
- 技术
---

#### 新年快乐！

纯Js实现的烟花特效
<!-- more -->

```javascript
//运动轨迹
  function getStyle(obj, attr) {
    if (window.getComputedStyle) {
      return window.getComputedStyle(obj)[attr];
    } else {
      return obj.currentStyle[attr];
    }
  }
  function bufferMove(obj, json, fn) {
    let speed = 0;
    clearInterval(obj.timer);
    obj.timer = setInterval(function () {
      var flag = true;
      for (var attr in json) {
        var currentValue = null;
        if (attr === "opacity") {
          currentValue = Math.round(getStyle(obj, attr) * 100);
        } else {
          currentValue = parseInt(getStyle(obj, attr));
        }
        speed = (json[attr] - currentValue) / 10;
        speed = speed > 0 ? Math.ceil(speed) : Math.floor(speed);

        if (currentValue !== json[attr]) {
          if (attr === "opacity") {
            obj.style.opacity = (currentValue + speed) / 100;
            obj.style.filter = "alpha(opacity=" + (currentValue + speed) + ")"; //IE
          } else {
            obj.style[attr] = currentValue + speed + "px";
          }
          flag = false;
        }
      }
      if (flag) {
        clearInterval(obj.timer);
        fn && typeof fn === "function" && fn();
      }
    }, 10);
  }
  class Firework {
    constructor(x, y) {
      //x,y鼠标的位置
      this.x = x; //将水平位置赋值给this.x属性。
      this.y = y; //将垂直位置赋值给this.y属性。
      this.ch = document.documentElement.clientHeight; //可视区的高度
    }
    init() {
      //1.创建烟花节点。
      this.firebox = document.createElement("div");
      this.firebox.style.cssText = `width:5px;height:5px;background:#fff;position:absolute;left:${this.x}px;top:${this.ch}px;`;
      document.body.appendChild(this.firebox);
      this.firemove(); //创建完成，直接运动。
    }
    //2.烟花节点运动
    firemove() {
      bufferMove(this.firebox, { top: this.y }, () => {
        document.body.removeChild(this.firebox);
        //当烟花节点消失的时候，创建烟花碎片
        this.createfires();
      });
    }
    //3.当前鼠标点击的位置，随机产生20-40个盒子。(随机颜色)
    createfires() {
      for (let i = 1; i <= this.rannum(20, 40); i++) {
        this.fires = document.createElement("div");
        this.fires.style.cssText = `width:2px;height:4px;background:rgb(${this.rannum(
          0,
          255
        )},${this.rannum(0, 255)},${this.rannum(
          0,
          255
        )});position:absolute;left:${this.x}px;top:${this.y}px;`;
        document.body.appendChild(this.fires);
        this.fireboom(this.fires); //设计成一个一个运动，等到循环结束，出现整体结果。
      }
    }
    //4.烟花碎片运动。
    fireboom(obj) {
      //存储当前obj的初始值。
      let initx = this.x;
      let inity = this.y;

      //随机产生速度(水平和垂直方向都是随机的,符号也是随机的)。rannum决定烟花范围
      let speedx = parseInt(
        (Math.random() > 0.2 ? "-" : "") + this.rannum(1, 5)
      );
      let speedy = parseInt(
        (Math.random() > 0.2 ? "-" : "") + this.rannum(1, 5)
      );

      obj.timer = setInterval(() => {
        initx += speedx;
        inity += speedy++; //模拟重力加速度(垂直方向比水平方向快一些)
        if (inity >= this.ch) {
          document.body.removeChild(obj);
          clearInterval(obj.timer);
        }
        obj.style.left = initx + "px";
        obj.style.top = inity + "px";
      }, 1000 / 60);
    }
    //随机区间数
    rannum(min, max) {
      return Math.round(Math.random() * (max - min) + min);
    }
  }

  document.onclick = function (ev) {
    var ev = ev || window.event;
    //ev.clientX,ev.clientY//获取的鼠标的位置
    new Firework(ev.clientX, ev.clientY).init();
  };

```