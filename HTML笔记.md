

## 1. 初识HTML

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

## 2. 基本标签
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

## 3. 图像标签
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

## 4. 超链接标签
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

## 5. 行内元素和块元素

* 块元素
  * 无论内容多少，元素独占一行
* 行内元素
  * 左右都是行内元素的可以排在一行

## 6. 列表标签

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

## 7. 表格标签

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

## 8. 媒体元素 

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

## 9. 页面结构

| 元素名  |             描述             |
| :-----: | :--------------------------: |
| header  |      标题头部区域的内容      |
| footer  |      标记脚部区域的内容      |
| section |   Web页面中的一块独立区域    |
| article |        独立的文章内容        |
|  aside  | 相关内容或应用(常用于侧边栏) |
|   nav   |        导航类辅助内容        |

示例代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>页面结构分析</title>
</head>
    <body>
        <header><h2>网页头部</h2></header>
        <section><h2>网页主体</h2></section>
        <footer><h2>网页脚部</h2></footer>
    </body>
</html>
```

结果演示：

![demo6](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_HTML_Demo6.png)

## 10. iframe内联框架

```html
<iframe src="" name=""></iframe>
```

* src：引用页面地址
* name：框架标识名

示例代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>iframe内联框架</title>
</head>
    <body>
        <iframe
                src="//player.bilibili.com/player.html?aid=212189891&bvid=BV1ka411b76m&cid=548248234&page=1"
                name="hello"
                width="500"
                height="500"
                scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true">
        </iframe>
        <a href="5.列表.html" target="hello">点击跳转</a>
    </body>
</html>
```



结果演示：

![demo7](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_HTML_Demo7.png)

## 11. 表单

```html
表单标签(用于收集和提交信息)
分为两部分:
    1.form标签:用于标识表单范围，可以设置数据提交的相关信息

    2.其他表单控件:表单内部的输入框、按钮等相关标签.
        1.input输入表单元素
            <input>单标签
            type属性可以设置不同的属性来指定不同的类型(提交按钮、输入框等)
            <input type="属性值">
            属性值                      表述
            button                      定义点击按钮(通常通过javascript启动脚本)
            checkbox                    复选框
            file                        输入字段和“浏览”按钮，供文件上传
            hidden                      隐藏输入的字段
            image                       图像形式的提交按钮
			readonly					只读不能修改
			disable						禁用
            password                    密码字段，该字段的字符被掩码
            radio                       定义单选按钮
            reset                       定义重叠按钮，重叠按钮会清除表单中的所有数据
            submit                      定义提交按钮，提交按钮会把表单数据发送到服务器
            text                        定义单行的输入字段，用户可在其中输入文本，默认为20个字符

            除type外其他的属性
            属性                        属性值                      表述
            name                        用户自定义                  定义input元素的名称
            value                       用户自定义                  input元素的值
            checked                     checked                    规定input元素首次加载时应该被选中
            maxlength                   正整数                      规定输入字段中字符的最大长度
            size                        正整数                      指定表单元素的初始宽度

        2.select下拉表单元素
            在页面中如果有多个选项让用户选择,且想要节约页面空间时，可以用selec标签定义下拉列表
            标签特点:
                    1.<select>中至少包含一对<option>
                    2.<option>中设置属性selected="selected"时，当前选项为默认选中项
            书写格式:
                    <select>
                        <option> 选项1 </option>
                        <option> 选项2 </option>
                        ...
                    </select>

        3.textarea文本域元素
            input标签只是单行显示，只适用于少量内容输入,输入过多文本(需要换行)用textarea标签
            书写格式:
                    只是设置框体
                    <textarea cols="列数" row="行数(整数)">
                        文本内容
                    </textarea>

        4.label标签
        <label>标签为input元素定义标注
        用于绑定一个表单元素，当点击<label>标签内文本时，浏览器就会自动将焦点（光标）转到或者选择对应的表单元素上,增加使用体验
        特点:<label>标签的for属性应当与相关元素的id属性相同
        书写格式:
                <label for="id属性">男</label>
                ------或者直接用标签包裹------
                <label>内容</label>
```

1. post与get

   * get：可以再url中看到提交的信息(高效)

   * post：传输大文件，url无法查看道提交的信息

   示例代码：

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>登陆注册</title>
   </head>
       <body>
           <h1>注册</h1>
           <!--表单form
               action: 表单提交的位置，可以是网站也可以是一个请求处理地址
               method: post,get 提交方式
           -->
           <form action="7.媒体元素.html" method="post">
               <!--文本输入框：input type="text”-->
               <p>名字：<input type="text" name="username"></p>
               <!--密码输入框：input type="password”-->
               <p>密码：<input type="password" name="password"></p>
   
               <!--提交-->
               <input type="submit">
               <!--重置-->
               <input type="reset">
           </form>
       </body>
   </html>
   ```

2. 文本框和单选框

   ```html
               <!--单选框标签
                   name: 实现单选
                   vale: 单选框的值
               -->
               <p>性别：
                   <input type="radio" value="boy" name="sex"> 男
                   <input type="radio" value="girl" name="sex"> 女
               </p>
   ```

   

3. 按钮和多选框

   ```html
   			<!--多选框-->
               <p>
                   <input type="checkbox" value="sleep" name="hobby"> 睡觉
                   <input type="checkbox" value="code" name="hobby" checked> 敲代码
                   <input type="checkbox" value="chat" name="hobby"> 聊天
               </p>
               <!--按钮-->
               <p>
                   <input type="button" name="btn1" value="点击">
                   <input type="image" src="麻衣学姐.jpg" width="50" height="50">
               </p>
   ```

   

4. 列表框文本域和文件域

   ```html
               <!--下拉框，列表框-->
               <p>
                   <select name="列表名称">
                       <option value="选项值">选项1</option>
                       <option value="china" selected>中国</option>
                       <option value="US">美国</option>
                       <option value="Swiss">瑞士</option>
                   </select>
               </p>
               <!--文本域-->
               <p>
                   反馈：
                   <textarea name="textarea" cols="50" rows="10">文本内容</textarea>
               </p>
               <!--文件域-->
               <p>
                   <input type="file" name="files">
               </p>
   ```

   

5. 搜索框滑块与简单验证

   ```html
               <!--邮件验证-->
               <p>
                   <input type="email" name="email">
               </p>
               <!--url验证-->
               <p>
                   <input type="url" name="url">
               </p>
               <!--数字验证
                   max 最大值
                   min 最小值
                   step 步长
               -->
               <p>
                   <input type="number" name="num" max="100" min="0" step="2">
               </p>
               <!--滑块-->
               <p>
                   音量：
                   <input type="range" name="voice" min="0" max="100">
               </p>
               <!--搜索框-->
               <p>
                   <input type="search" name="search">
               </p>
   ```

   

6. 表单应用

   ```html
               <!--增强鼠标可用性-->
               <p>
                   <label for="mark">点击试试</label>
                   <input type="text" id="mark">
               </p>
   ```

   

7. 表单的初级验证

   * placeholder：用于提示一些信息

   * required：不能为空

   * pattern：正则表达式  [常用正则表达式](https://www.jb51.net/tools/regex.htm)

     

   ```html
               <!--提示信息-->
               <p>
                   <input type="text" placeholder="提示" required>
               </p>
               <!--自定义邮箱-->
               <p>
                   <input type="text" name="diyemail" pattern="/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/">
               </p>
   
   ```

   

结果演示：

![demo8](https://cdn.jsdelivr.net/gh/cxy20219/image/images/Demo_HTML_Demo8.png)

