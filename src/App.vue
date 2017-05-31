<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor
    },
    data() {
      return {
        interval: 25,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* 前辈您好，我是徐人杰 
* 感谢您在百忙之中浏览我的简历。
*/

/* 首先给所有元素加上过渡效果 */
* {
  -webkit-transition: all .3s;
  transition: all .3s;
}
/* 白色背景太单调了，我们来点背景 */
html {
  color: rgb(222,222,222); background: rgb(0,43,54); 
}
/* 文字离边框太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 45vw; height: 90vh;
}
/* 代码高亮 */
.token.selector{ color: rgb(133,153,0); }
.token.property{ color: rgb(187,137,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(42,161,152); }

/* 加点 3D 效果呗 */
html{
  -webkit-perspective: 1000px;
          perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0; 
  -webkit-transition: none; 
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 接下来我给自己准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 48vw; height: 90vh; 
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
/* 好了，我开始写简历了 */


`,
          `
/* 这个简历好像差点什么
 * 对了，这是 Markdown 格式的，我需要变成对 HR 更友好的格式
 * 简单，用开源工具翻译成 HTML 就行了
 */
`
          ,
          `
/* 再对 HTML 加点样式 */
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;            
  content: counters(section, ".") " ";  
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`],
        currentMarkdown: '',
        fullMarkdown: `# 我的名字：徐人杰
# 我的联系方式：
### 手机：15279102530
### 邮箱：2578370399@qq.com || renjiexu96@gmail.com
### qq/wechat: 25787370399 , xrj1996kk
----
# 我的教育经历：
江西财经大学 本科  软件工程 2018年毕业（预计）

台湾长荣大学（交换生） 资讯工程 2016年结束

----

# 项目经验：

[麦当劳那么大甜筒半价抢](http://wz.jxhaiyinmcd.com/?r=weixin/process/extension&extension=PhoneCoupon&do=index&aid=1)

负责前端的H5页面开发，并与后端沟通（2017.05 - 2017.05）
 产品为同时使用在移动端包括微信产品, 工作性质为兼职外包,个人角色为 前端开发工程师。
1.还原设计稿，完成psd切图
2.使用flexiale的兼容方案与媒体查询相结合处理自适应问题。
3.配合后端使用JS-SDK实现分享功能。

# ----
我的书单：

1. 《javascript高级程序设计》 完成度：50%
2.《你不知道的javascript》上卷 完成度： 80%
3.《javascript设计模式与开发实践 By：AlloyTeam》完成度：20%
4.《ES6标准入门 By：阮一峰》完成度：60%
5.《javascript DOM编程艺术》完成度：90%
6.《Node js in action》完成度：70%
7.《HTTP权威指南》完成度：10%

--------
** 技术栈：Vue + js + html + css + nodejs+ mongoDB + 微信小程序 **
# 技能描述：

1. html5、css3：熟练掌握前端界面html5、css3开发。
深入理解html5标签的使用代码结构及语义化。
css熟悉使用过sass、stylus，熟练使用css3动画弹性布局等现代布局方式，
掌握mintUI、semanticUI、bootstrap3、WEUI框架开发，
有多个pc跟移动设备界面开发经验，目前正在学习最新的grid布局。
2. javascript：熟悉ES6、熟练掌握JavaScript原生编程和jqury编程
、DOM编程，理解并实践封装，理解JavaScript的原型链机制
基本掌握JavaScript面向对象的编程原理，
能够在编程中实践一些设计模式的思维，了解函数式编程。
正在初步入门学习新一代的typescript。
3. Node：熟练使用npm、yarn包工具，熟练搭建node环境，
可实现服务器搭建、爬虫、文件流处理、数据库操作、gulp使用，
掌握使用express、koa框架，理解后端路由和中间件，
能够通过node实现mvc + mongoDB的express应用，
希望在工作中更加系统深入学习这块知识。
4. MVVM：熟练掌握Vue编程，初步理解底层原理，数据绑定，
前端History路由，了解MVVM开发模式，数据驱动的开发，
熟悉vue周边生态插件使用、
熟练掌握vue-cli全家桶：vue-component、vue-router、axios、vue-resource、
mintUI、elementUI开发熟练掌握vue组件化思维开发。
并有微信小程序的较完整的实战开发经验。
希望在工作中继续深入学习nuxt和react。
5. 其他：掌握使用gulp、能使用mongoDB和mysql，
有java面向对象的学习经历，java操作数据库的基础，
和j2ee MVC的初级基础。熟练使用ps工具，
及摄影技术（哈哈，混入了= =）。
6. 基础：有计算机基础，了解计算机组成原理，
学习过计算机网络线性代数和离散数学，
了解HTTP的URL、报文（组成、请求方法、状态码、首部）、
TCP三次握手。有数据结构和简单算法的基础，
初步了解复杂度和性能，熟练使用递归、多种排序、查找。
----
# 校内经历
1. 交换生经历：被选为优秀交换生赴台湾长荣大学资讯工程学院进行学习。（2015年-2016年）
2. 大学生创业竞赛：“Unity约拍” 校园服务性产品获得国家级评比资格并获取20000元启动资金，目前已盈利12000余元，
在团队中负责app开发和摄影项目运营。（2015年-2017年（年底结题））
3. 热爱篮球，作为副队长带领学院篮球取得全校四强的战绩，哈哈，曾经梦想进入NBA，落入凡尘写代码。
4. 用友创新之星奖学金（1/60）、先进个人奖学金。


# 我的链接
----

* [GitHub](https://github.com/renjie1996)
* [我的掘金](https://juejin.im/user/58abc837ac502e007e89aed4)

> [参考](https://github.com/jirengu-inc/animating-resume) 终生学习，至死方休！

`
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0)
        await this.progressivelyShowResume()
        await this.progressivelyShowStyle(1)
        await this.showHtml()
        await this.progressivelyShowStyle(2)
      },
      showHtml: function () {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) { return }
            // 计算前 n 个 style 的字符总数
            let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
            let prefixLength = length - style.length
            if (this.currentStyle.length < length) {
              let l = this.currentStyle.length - prefixLength
              let char = style.substring(l, l + 1) || ' '
              this.currentStyle += char
              if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                this.$nextTick(() => {
                  this.$refs.styleEditor.goBottom()
                })
              }
              setTimeout(showStyle, interval)
            } else {
              resolve()
            }
          }).bind(this)
          showStyle()
        })
      },
      progressivelyShowResume() {
        return new Promise((resolve, reject) => {
          let length = this.fullMarkdown.length
          let interval = this.interval
          let showResume = () => {
            if (this.currentMarkdown.length < length) {
              this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
              let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
              let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
              console.log(prevChar)
              if (prevChar === '\n' && this.$refs.resumeEditor) {
                this.$nextTick(() => this.$refs.resumeEditor.goBottom())
              }
              setTimeout(showResume, interval)
            } else {
              resolve()
            }
          }
          showResume()
        })
      }
    }
  }

</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  
  html {
    min-height: 100vh;
  }
  
  * {
    -webkit-transition: all .3s;
    transition: all .3s;
  }
</style>
