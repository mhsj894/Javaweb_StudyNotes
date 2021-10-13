# 今日

1. web概念概述
2. HTML



## web概念概述

* JavaWeb：
  * 使用Java语言开发基于互联网的项目
* 软件架构：
  1. C/S：Client/Server 客户端/服务器端
     * 在用户本地有一个客户端，在远程有一个服务器程序
     * 如：QQ，迅雷...
     * 优点：
       1. 用户体验好
     * 缺点：
       1. 开发、安装、部署、维护 麻烦
  2. B/S：Browser/Server 浏览器/服务器端
     * 只需要一个浏览器，用户通过不同的网址（URL），客户访问不同的服务器端程序
     * 优点：
       1. 开发、安装、部署、维护 简单
     * 缺点：
       1. 如果应用过大，用户的体验可能受到影响
       2. 对硬件要求过高
* B/S结构详解
  * 资源分类：
    1. 静态资源：
       * 使用静态网页开发技术开发发布的资源。
       * 特点：
         * 所有用户访问，得到的结果是一样的。
         * 如：文本，图片，音频，视频，HTML，CSS，JavaScript
         * 如果用户请求的是静态资源，那么服务器会直接将静态资源发送给浏览器，浏览器中内置了静态资源的引擎，可以展示静态资源
    2. 动态资源：
       * 使用动态网页及时发布的资源。
       * 特点：
         * 所有用户访问，得到的结果可能不一样。
         * 如：jsp/servelt，php，asp...
         * 如果用户请求的是动态资源，那么服务器执行动态资源，转换为静态资源，再发送给浏览器
  * 我们要学习动态资源：
    * HTML：用于搭建基础网页，展示页面的内容
    * CSS：用于美化页面，布局页面
    * JavaScript：控制页面的元素，让页面有一些动态的效果

## HTML

1. 概念：是最基础的网页开发语言
   * Hyper Text Markup Language 超文本标记语言
     * 超文本：
       * 超文本是用超链接的方法，将各种不同空间的文字信息组织在一起的网状文本。
     * 标记语言：
       * 由标签构成的语言。<标签语言> 如 HTML，XML
       * 标记语言不是编程语言

2. 快速入门

   * 语法：

     1. html文档后缀名 .html或者.htm

     2. 标签分为

        1. 围堵标签：有开始标签和结束标签。如<html> </html>
        2. 自闭和标签：开始标签和结束标签在一起。如<br/>

     3. 标签可以嵌套：

        1. 需要正确嵌套，不能你中有我，我中有你
        2. 错误：<a> <b> <a> <b>
        3. 正确：<a> <b> <b> <a>

     4. 在开始标签中可以定义属性。属性由键值对构成，值需要用引号（单双）引起来

     5. HTML的标签不区分大小写，但建议使用小写

        ``` html
        <html>
            <head>
                <title>HelloWorld</title>
            </head>
        
            <body>
                <font color='red'>Hello World</font>
                <br/>
                <font color='green'>Hello World</font>
            </body>
        </html>
        ```

        

3. 标签

   1. 文件标签：构成HTML最基本的标签
      * <html ：html文档的根标签
      * <head ：头标签。用于指定html文档的一些属性。引入外部的资源
      * <title ：定义标题标签
      * <body ：体标签
      * < !DOCTYPE html  ：html5中定义该文档是html文档
      
   2. 文本标签：和文本有关的标签
      * 注释：!-- 注释内容 --
      * h1-h6：标题标签
        * h1-h6：字体大小逐渐递减
      * p：段落标签
      * br：换行标签
      * hr：展示一条水平线
        * 属性：
          * color：颜色
          * width：宽度
          * size：高度
          * align：对齐方式
            * center：居中
            * left：左对齐
            * right：右对齐
      * b：字体加粗
      * i：斜体
      * font：字体标签
        * 属性：
          * color：颜色
          * size：大小
          * face：字体
          * center：
      * 属性定义：
        * color：
          1. 英文单词：red，green，blue
          2. rgb(值1，值2，值3)：值的范围：0-255 如rgb(0,0,255)
          3. #值1值2值3：值的范围：00-FF。如：#FF00FF
        * width：
          1. 数值：width='20'，数组的单位，默认是px(像素)
          2. 数组%：占比相对于父元素的比例
      * 案例：公司简介

   3. 图片标签：

      ``` html
      <!--展示一张图片 img-->
          <img src="image/3.jpg" alt="图片" align="center" height="auto" width="500">
      
          <!--
          相对路径
              * 以.开头的路径
                  * ./：代表当前目录
                  * ../：代表后退上一级目录
          -->
          <img src="./image/4.png" alt="图片" height="auto" width="500">
          <img src="./image/../image/1.png" alt="图片" height="auto" width="500">
      ```

      

   4. 列表标签：

      * 有序列表：
        * ol：
        * li：
      * 无序列表：
        * ul：
        * li：

   5. 链接标签：

      * a：定义一个超链接
        * 属性：
          * href：指定访问资源的URL(统一资源定位符)
          * target：指定打开资源的方式
            * _self：默认值，在当前页面打开
            * _blank：在空白页面打开

   6. div和span：

      ``` html
      <!--
          div：每一个div占满一整行，块级标签
          span：文本在一行标签，行内标签 内联标签
      -->
      <span>马猴烧酒</span>
      <span>八九寺</span>
      <hr>
      <div>马猴烧酒</div>
      <div>八九寺</div>
      ```

      

   7. 语义化标签：html5中为了提供程序可读性提供的标签

      1. header：页眉
      2. footer：页脚

   8. 表格标签：

      * table：定义表格

        * width：宽度
        * border：边框
        * cellpadding：定义内容与单元格的距离
        * cellspacing：定义单元格之间的距离。如果定义为0，则单元格之间的线会合为一条
        * bgcolor：背景色
        * align：对齐方式

      * tr定义行

        * bgcolor：背景色
        * align：对齐方式

      * td：定义单元格

        * colspan：合并行

        * rowspan：合并列

      * th：定义表头单元格

      * caption：表格标题

      * thead：表示表格的头部分

      * tbody：表示表格的体部分

      * tfoot：表示表格的脚部分

## 案例：旅游网站首页

1. 确定使用table来完成布局
2. 如果某一行只有一个单元格，则使用tr里嵌套td
3. 如果某一行有多个单元格，则使用tr>td>table

