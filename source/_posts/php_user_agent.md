---
title: 判断当前访问设备以及浏览器版本
date: 2018-01-11 11:18:34
tags:
---
根据项目需求判断Web客户端访问设备类型，从而根据不同的设备（pc or mobile）来为用户导向不同的url，下面为PHP和Js实现的部分代码示例。
<!-- more -->
###### Web客户端访问设备类型判断方法-php
```php
function getDeviceType() {
    //通过user agent获取当前访问设备信息，并将字符串转化为小写
    $agent = strtolower($_SERVER['HTTP_USER_AGENT']);
    //分析数据，判断当前设备类型
    $is_iphone = !!(strpos($agent, 'iphone'));
    $is_android = !!(strpos($agent, 'android'));
    $is_iPod = !!(strpos($agent, 'ipod'));
    //获取当前路径
    $uri = $_SERVER["REQUEST_URI"];
    $key = 'from=wap';
    $check = strpos($uri,$key);
    //pc端访问返回「pc」，移动端访问一般返回「mobile」，若移动端访问路径含有from=wap返回「pc」
    if ($is_iphone || $is_android || $is_iPod) {
        $type = $check ? 'pc': 'mobile';
    } else {
        $type = 'pc';
    }
    return $type;
}
$type = getDeviceType();
if ($type === 'mobile') {
    redirect('//'.$url);
} else {
    redirect('//'.$url);
}
```
###### Web客户端访问设备类型判断方法-Js
```js
function getDeviceType () {
    //获取当前访问设备的信息，并将字符串转化为小写
    let UserAgent = navigator.userAgent.toLowerCase();
    //分析数据，判断当前设备类型
    let is_iphone = !!(UserAgent.indexOf('iphone') > -1)
    let is_android = !! (UserAgent.indexOf('android') > -1)
    let is_ipod = !!(UserAgent.indexOf('ipod') > -1)
    //获取当前路径
    let uri = location.href;
    let key = 'from=wap'
    let check = !!(uri.indexOf(key) > -1)
    let type = '';
    //pc端访问返回「pc」，移动端访问一般返回「mobile」，若移动端访问路径含有from=wap返回「pc」
    if (is_iphone || is_android || is_ipod) {
        type = check ? 'pc': 'mobile';
    } else {
        type = 'pc';
    }
}
let type = getDeviceType();
if  (type === 'mobile') {
    location.href = ""
} else {
    location.href = ""
}
```
###### Web客户端浏览器版本判断-Js
```js
function getBrowserVersion () {
    //sys的key为浏览器类型，value为浏览器版本
    let sys = {};
    //获取当前访问的浏览器信息并将字符串转化为小写
    let UserAgent = navigator.userAgent.toLowerCase();
    //判断浏览器版本
    (browserInfo = UserAgent.match(/msie ([\d.]+)/)) ? sys.ie = browserInfo[1] :
    (browserInfo = UserAgent.match(/firefox\/([\d.]+)/)) ? sys.firefox = browserInfo[1] :
    (browserInfo = UserAgent.match(/chrome\/([\d.]+)/)) ? sys.chrome = browserInfo[1] :
    (browserInfo = UserAgent.match(/opera.([\d.]+)/)) ? sys.opera = browserInfo[1] :
    (browserInfo = UserAgent.match(/version\/([\d.]+).*safari/)) ? sys.safari = browserInfo[1] : 0;
    return sys;
}
//低于10的IE版本跳转到browser.html页面
if (getBrowserVersion().ie && Number(getBrowserVersion().ie) < 10) {
    window.location.href = "/browser.html";
}
```