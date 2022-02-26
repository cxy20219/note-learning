## 01. 初识HTML
>Hyper Text Markup Language（超文本标记语言）
主题框架：
```html
表示用的HTML5版本显示网页
<!DOCTYPE>
<html>主体
    <!--网页头部-->
    <head>
        <!--meta标签描述网站的一些信息-->
        <!--meta一般用来做 SEO-->
        <meta name="旅程@的小窝">
        <!--网页标题-->
        <title> 网页标题 </title>
    </head>
    <!--网页主题-->
    <body>
        网页主要内容
    </body>
</html>
```
---
>向世界问好
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>旅程@的小窝</title>
</head>
    <body>
        hello world
    </body>
</html>
```
结果展示：  

![Demo1](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_HTML_Demo1.png) 
---

## 02. 基本标签
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>基本标签</title>
</head>
    <body>
        <!--标题标签(文字会加粗):6个等级<h1>到<h6> 字号也会依次变小 h1最大-->
        <h1>一级标签</h1>
        <h2>二级标签</h2>
        <h3>三级标签</h3>
        <h4>四级标签</h4>
        <h5>五级标签</h5>
        <h6>六级标签</h6>

        <!--段落标签:<p>标签定义段落段与段之间有层次感-->
        <p>段落一</p>
        <p>段落二</p>

        <!--水平线标签:<hr> 单标签-->
        <hr>

        <!--换行标签:<br> 单标签-->
        <br>

        <!--粗体，斜体-->
        粗体：<strong>hello world</strong>
        <br>
        斜体：<em>hello world</em>

        <!--特殊符号:一般形式 &xxx;-->
        <p>空格:&nbsp;hello world</p>
        <p>&copy;版权所有 旅程@</p>
    </body>
</html>
```
特殊字符参照表：[https://tsfhdq.com/568.html](https://tsfhdq.com/568.html)

结果演示：

![Demo2](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_HTML_Demo2.png)

## 03. 图像标签
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>图像标签学习</title>
</head>
    <body>
    <!--
        src : 图片地址
        图片标签:
        1.可以有多个属性，在标签名后面
        2.属性之间没有先后顺序，标签名与属性，属性与属性之间均以空格分开
        3.属性采取键值对的格式,例如key="value" 属性="属性值"
        书写格式: <img src="图片地址" alt="图片描述" title="悬停文字">
        地址:
        1.相对路径:同级路径 <img src="baidu.gif"/> 下一级路径<img src="imges/baidu.gif"/>  上一级路径（上一级文件里的图片）<img src="../baidu.gif">
        2.绝对路径:直接给出完整地址,或者完整的网络地址
    -->
        <img src="https://tse2-mm.cn.bing.net/th/id/OIP-C.NdWpnJQWKmexmoN4lJARLAHaNK?pid=ImgDet&rs=1" alt="麻衣学姐" title="悬停文字">
    </body>
</html>
```

## 04. 超链接标签
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>链接标签</title>
</head>
    <body>
        <!--标记-->
        <a name="top">顶部</a>
        <!--
            超链接标签:
            <a>标签用于定义一个超链接，作用是从一个页面到另一个页面
            书写格式；<a href="跳转地址" target="新窗口弹出方式"> 文本内容或图片</a>
            href :用于指定连接目标的url地址
            target :用于指定连接页面的打开方式,其中_self为默认值(不打开新窗口)，_blank在新窗口打开
        -->
        <a href="https://www.baidu.com/?tn=80035161_1_dg" target="_self">默认打开窗口跳转到百度首页</a>
        <br>
        <a href="https://www.baidu.com/?tn=80035161_1_dg" target="_blank">新窗口打开百度首页</a>
        <img src="https://pic1.zhimg.com/v2-d58ce10bf4e01f5086c604a9cfed29f3_r.jpg?source=1940ef5c">
        <!--
            锚链接：
            1. 需要一个标记
            2. 跳转到标记
        -->
        <a href="#top">回到顶部</a>

        <!--
            功能性链接
            1. 邮件链接: mailto
            2. qq链接
        -->
        <a href="mailto:1730368162@qq.com">点击联系</a>
        <a target="_blank" href="http://wpa.qq.com/msgrd?v=3&uin=&site=qq&menu=yes">
            <img border="0" src="http://wpa.qq.com/pa?p=2::53" alt="你好，加我领取" title="你好，加我领取"/>
        </a>
    </body>
</html>
```

## 05. 行内元素和块元素

* 块元素
  * 无论内容多少，元素独占一行
* 行内元素
  * 左右都是行内元素的可以排在一行

## 06. 列表标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>列表学习</title>
</head>
    <body>
        <!--
            有序列表:
            <ol></ol> 列表项用<li></li>
            一样有默认样式 但一般用css进行设置
         -->
        <ol>
            <li>Java</li>
            <li>python</li>
            <li>c/c++</li>
        </ol>
        <hr>
        <!--
            无序列表：
            没有顺序之分  <ul></ul> 中只能镶嵌<li></li>,不可设置其他标签文字
            无序列表有默认的样式 但一般用css进行设置
        -->
        <ul>
            <li>Java</li>
            <li>python</li>
            <li>c/c++</li>
        </ul>
        <hr>
        <!--
            自定义列表:
            与无序列表有点类似 但是自定义列表有列表标题和列表项两部分
            书写格式:定义列表<dl></dl>  列表标题<dt></dt>  列表项<dd></dd>
            标题与列表项没有数量限制
        -->
        <dl>
            <dt>学科</dt>
            <dd>Java</dd>
            <dd>python</dd>
            <dd>c/c++</dd>
            <dt>位置</dt>
            <dd>重庆</dd>
            <dd>西安</dd>
            <dd>成都</dd>
        </dl>
    </body>
</html>
```

结果演示：

![demo3](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_HTML_Demo3.png)

## 07. 表格标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>表格学习</title>
</head>
    <body>
        <!--
            表格分为表头和表体
            表格标签书写格式:
            <table>
                <thead>
                    <tr>
                        <th>表头单元格的内容</th>
                        ...
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>表体单元格的内容</td>
                        ...
                    </tr>
                    ...
                </tbody>
            </table>
            表格属性:
                属性名             属性值               描述
                align             left、center、right   表格相对周围元素对齐的方式
                border            "1"或""               表格是否拥有边框,默认为"",没有边框
                cellpadding       像素值                单元格与其内容的空白,默认为1像素
                cellspacing       像素值                单元格之间的空白,默认为2像素
                width             像素值或百分比         规定表格的宽度

            合并单元格:
                跨行合并:rowspan="合并的单元格数"(合并行)
                跨列合并:colspan="合并的单元格数"(合并列)
        -->
        <table border="1" cellpadding="5px">
            <thead>
            <tr>
                <th>姓名</th>
                <th>性别</th>
                <th>年龄</th>
            </tr>
            </thead>
            <tbody>
            <tr>
                <td>张三</td>
                <td>男</td>
                <td>18岁</td>
            </tr>
            <tr>
                <td>冯宝宝</td>
                <td>女</td>
                <td>18岁</td>
            </tr>
            <tr>
                <td>王也</td>
                <td>男</td>
                <td>19岁</td>
            </tr>
            </tbody>
        </table>
        <br>
        <hr>
        <table border="1">
            <thead>
            <tr>
                <th rowspan="2"> 第一行第一个</th>
                <th>第一行第二个</th>
                <th>第一行第三个</th>
                <th>第一行第四个</th>
            </tr>
            <tr>
                <th colspan="2">第二行第二个</th>
                <th>第二行第三个</th>
            </tr>
            </thead>
        </table>
    </body>
</html>
```

结果演示：

![demo4](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_HTML_Demo4.png)

## 08. 媒体元素 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>媒体元素学习</title>
</head>
    <body>
        <!--
            音频和视频
            src:资源路径
            controls:控制条
            autoplay:自动播放
        -->
        <video src="test.mp4" controls autoplay></video>

        <hr>

        <!--音频-->
        <audio src="test_audio.mp3" controls ></audio>
</html>
```

结果演示：

![demo5](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_HTML_Demo5.png)