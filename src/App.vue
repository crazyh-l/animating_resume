
<template>
  <div class="body">
     <styleEditor ref="styleEditor" :code="currentStyle"></styleEditor>
     <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
     <Life ref="life"></life>
  </div>
</template>

<script>
import StyleEditor from './components/StyleEditor'
import ResumeEditor from './components/ResumeEditor'
import Life from './components/Life'
import  Velocity from 'velocity-animate'
import './assets/reset.css'

export default {
  name: 'app',
  
  components: {
    StyleEditor,
    ResumeEditor,
    Life
  },
  data() {
    return {
      interval: 40,
      currentStyle:'',
      enableHtml: false,
      fullStyle: [
          `/*
* Inspired by http://strml.net/
* 大家好，我是杨浩
* 快要过年了，好多公司都在招聘，你是不是也在准备简历呀。
* 说做就做，我也来写一份简历！
*/

/* 首先给所有元素加上过渡效果 */
* {
  transition: all .3s;
}
/* 白色背景太单调了，我们来点背景 */
html {
  color: rgb(222,222,222); background: #3d3536;
}

/* 文字离边框太近了 */
.styleEditor {
  position:fixed;
  padding: .5em;
  border: 1px solid;
  margin: 1em;
  overflow: auto;
  width: 45vw; height: 90vh;
  border-radius:4px;
}
/* 代码高亮 */
.token.selector{ color: rgb(133,153,0); }
.token.property{ color: rgb(187,137,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(42,161,152); }


/* 接下来我给自己准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: 1em;
  width: 48vw; height: 90vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
  border-radius:4px;
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
/*好了，简历写完了，我再来画一个小网页*/
.resumeEditor{
  display: none;
}
.life{
    display:block;
    position: absolute; right: 0; top: 0;
    margin: 1em;
    width: 48vw; height: 90vh;
    border: 1px solid;
    background: white; color: #222;
    overflow: auto;
    border-radius:4px;
    
  }

  /*这样看是不是很别扭，没关系，放大点吧！*/
  
`,`
  .life{
    display:block;
    position: absolute; right: 0; top: 0;
    margin: 1em;
    width: 48vw; height: 90vh;
    border: 1px solid;
    background: white; color: #222;
    overflow: auto;
    border-radius:4px;
  }
  .styleEditor{
    display:none;
  }

  .life{
    padding:0;
    margin:0;
    display:block;
    width: 100%; height: 100%;
    border: 1px solid;
    background: white; color: #222;
    padding:0;
    margin:0;
  }

`],
        currentMarkdown: '',
        fullMarkdown: `

## 个人信息

 - 杨浩/男/1993 03/25 
 - 专科/西南科技大学
 - 工作年限：1年
 - Github：https://github.com/97413192
 - 期望职位：java初级程序员，后台开发
 - 期望薪资：税前月薪6k
 - 期望城市：成都
 - 联系方式：13551541292 
 - QQ :97413192
----


技能
----


- Web开发：java
- Web框架：java/spring/springmvc/springboot
- 前端框架：Bootstrap/Layui/
- 前端工具：webpack
- 数据库相关：MySQL/SQLServer
- 版本管理：Svn/Git
- 单元测试：JUnit

工作经历
----

2017-06 ~ 2018-03 


  
## 成都微鑫通时代科技有限公司 （ 2017年3月 ~ 2018年1月 ）

### 安徽三员分离项目 
之后在写

### 芒市德宏州项目 
之后在写



链接
----

> 如果你喜欢这个效果，Fork [我的项目](https://github.com/97413192/animating_resume)，打造你自己的简历！

`
      }
    },
    created() {
      var userAgent = window.navigator.userAgent; 
      var ie = this.isIE(userAgent);
      if (ie !== false) {
        alert('您使用的是ie浏览器'+ isIE +'版本，可能效果不太好哦！');
      }
      this.makeResume()
    },
     methods: {
      isIE:  function (userAgent) {
        //判断是否是ie浏览器，因为ie效果不太好
        var UA = userAgent || navigator.userAgent;
        if(/msie/i.test(UA)) {
          return UA.match(/msie (\d+\.\d+)/i)[1];
        } else if(~UA.toLowerCase().indexOf('trident') && ~UA.indexOf('rv')) {
          return UA.match(/rv:(\d+\.\d+)/)[1];
        }
        return false;
      },
      makeResume: async function () {
        await this.progressivelyShowStyle(0)
        await this.progressivelyShowResume()
        await this.progressivelyShowStyle(1)
        await this.showHtml()
        await this.progressivelyShowStyle(2)
        await this.progressivelyShowStyle(3)
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
.body{
    height: 100%;
 }
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  html {
    min-height: 100vh;
  }
  *{
    box-sizing: border-box;
  }
</style>
