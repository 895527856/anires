<template>
  <div id="app">
    <div id="content">
      <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
      <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
    <div id="foot">
      <ThankEditor ref="thankEditor" :markdown="currentThankMarkdown" :enableHtml="enableHtml"></ThankEditor>
    </div>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import ThankEditor from './components/ThankEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor,
      ThankEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* Inspired by http://strml.net/
* 源码地址 https://github.com/sitexa/anires
* 大家好，我是刘志萍。
* 我来写一份简历！
*/

/* 给所有元素加上过渡效果 */
* {
  transition: all .1s;
}
/* 设置背景颜色 */
html {
  color: rgb(222,222,222); background: rgb(0,64,64);
}
#content{
  height:70vh;
  margin:0;
}
#foot{
  height:29vh;
  margin:0;
}

/* 设置边框 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 50vw; height: 70vh;
  background: rgb(20,20,20);
}
/* 代码高亮 */
.token.selector{ color: rgb(130,150,0); }
.token.property{ color: rgb(190,140,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(40,160,150); }

/* 加3D效果 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 50vw; height: 70vh;
  border: 1px solid;
  background: rgb(200,200,200); color: #222;
  overflow: auto;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(-10deg) translateZ(-100px) ;
          transform: rotateY(-10deg) translateZ(-100px) ;
}
/* 开始写简历 */
`, `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
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
`, `/* 写封感谢信。
 * 感谢大家对我的关注。
 */
.styleEditor{
    width:50vw;height:70vh;
}

.resumeEditor{
   width:50vw;height:70vh;
}

.thankEditor{
  position: relative; left: 0; top: 0;
  background: #E9D9BB;
  color: #001C42;
  overflow: auto;
}

.thankEditor {
  width: 99vw; height: 45vh;
  border: 1px solid #ccc;
  font-size: .9em;
}
`,`
.thankEditor{
  padding: .5em;  margin: .5em; margin-top:1em;
}

.thankEditor ul,.thankEditor ol{
  list-style: none;
}
.thankEditor ul> li::before{
  content: '☞'; color: red;
  margin-right: .5em;
}
.thankEditor ol {
  counter-reset: section;
}
.thankEditor ol li::before {
  counter-increment: section;
  content: counters(section, "☞") " ";
  margin-right: .5em;
}

.thankEditor{
  width: 99vw; height: 45vh;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateX(-10deg) translateZ(-200px);
          transform: rotateX(-10deg) translateZ(-200px);
}

`],
        currentMarkdown: '',
        currentThankMarkdown: '',
        fullMarkdown: `南方
====
姓名：刘志萍
地点：广东深圳。

职业：软件工程师。

技能
====

数据库设计
----
  - 结构化数据库设计
  - noSQL设计

后端开发
----
  - 用户管理
  - 单点登录
  - 第三方登录
  - 权限管理
  - 交易系统
  - 支付系统
  - 社区系统
  - 博客系统
  - 移动开发
  
前端开发
----
  - Web前端开发

产品设计
----
  - 智慧旅游项目
  - p2p平台
  - 省级药品管理项目
  - 省级环境监控平台
  - 高速公路异地处罚系统
  - 环保局办公自动化系统
  - 保险公司数据迁移项目

技术及语言
----
  - Java: SpringMVC, SpringCloud, Hibernate, iBatis, springboot, play, spring
  - Kotlin: ktor, exposed, anko
  - Swift: Vapor, ReactiveSwift
  - Golang: hugo, beego, gorm, sqlx, matcha
  - Python: tushare, pandas, numpy, matplotlib
  - DotNet and PHP
  - DB: SQLServer, Oracle, MySQL/MariaDB, MongoDB, graphQL, redis, memcached, solr
  - WebServer: apache, nginx, tomcat, jetty
  - OS: CentOS, MacOS, Windows
  - Others: Docker, git, dubbo, activeMQ

工作经历
----

1. 上海万达信息股份有限公司
2. 深圳英迈思科技文化有限公司
3. 深圳组合科技有限公司


教育经历
----

1. 南昌大学 软件技术


网站
----

* [智慧物联运营中心](http://6395fe9b.ngrok.io/tourist-admin//index)
* [江西省药品综合管理系统](http://yz.jxhfpc.gov.cn/)
* [小鹿网](http://www.xiaoluwang.com)

链接
----

* [GitHub](https://github.com/895527856)
* [技术博客](https://i.csdn.net/#/uc/profile)


勾引方式
----

* 微信：toghter

`, thanksMarkdown: `
鸣谢
----

* 琵琶行 白居易 浔阳江头夜送客，枫叶荻花秋瑟瑟。主人下马客在船，举酒欲饮无管弦。醉不成欢惨将别，别时茫茫江浸月。
忽闻水上琵琶声，主人忘归客不发。寻声暗问弹者谁，琵琶声停欲语迟。移船相近邀相见，添酒回灯重开宴。千呼万唤始出来，犹抱琵琶半遮面。转轴拨弦三两声，未成曲调先有情。弦弦掩抑声声思，似诉平生不得志。低眉信手续续弹，说尽心中无限事。轻拢慢捻抹复挑，初为《霓裳》后《六幺》。大弦嘈嘈如急雨，小弦切切如私语。嘈嘈切切错杂弹，大珠小珠落玉盘。间关莺语花底滑，幽咽泉流冰下难。冰泉冷涩弦凝绝，凝绝不通声暂歇。别有幽愁暗恨生，此时无声胜有声。银瓶乍破水浆迸，铁骑突出刀枪鸣。曲终收拨当心画，四弦一声如裂帛。东船西舫悄无言，唯见江心秋月白。
沉吟放拨插弦中，整顿衣裳起敛容。自言本是京城女，家在虾蟆陵下住。十三学得琵琶成，名属教坊第一部。曲罢曾教善才服，妆成每被秋娘妒。五陵年少争缠头，一曲红绡不知数。钿头银篦击节碎，血色罗裙翻酒污。今年欢笑复明年，秋月春风等闲度。弟走从军阿姨死，暮去朝来颜色故。门前冷落鞍马稀，老大嫁作商人妇。商人重利轻别离，前月浮梁买茶去。去来江口守空船，绕船月明江水寒。夜深忽梦少年事，梦啼妆泪红阑干。
我闻琵琶已叹息，又闻此语重唧唧。同是天涯沦落人，相逢何必曾相识！我从去年辞帝京，谪居卧病浔阳城。浔阳地僻无音乐，终岁不闻丝竹声。住近湓江地低湿，黄芦苦竹绕宅生。其间旦暮闻何物？杜鹃啼血猿哀鸣。春江花朝秋月夜，往往取酒还独倾。岂无山歌与村笛？呕哑嘲哳难为听。今夜闻君琵琶语，如听仙乐耳暂明。莫辞更坐弹一曲，为君翻作《琵琶行》。感我此言良久立，却坐促弦弦转急。凄凄不似向前声，满座重闻皆掩泣。座中泣下谁最多？江州司马青衫湿。

  `
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0);
        await this.progressivelyShowResume();
        await this.progressivelyShowStyle(1);
        await this.showHtml();
        await this.progressivelyShowStyle(2);
        await this.progressivelyShowThanks();
        await this.progressivelyShowStyle(3)
      },
      showHtml() {
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
            if (!style) {
              return
            }
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
      },
      progressivelyShowThanks() {
        return new Promise((resolve, reject) => {
          let length = this.thanksMarkdown.length
          let interval = this.interval
          let showThanks = () => {
            if (this.currentThankMarkdown.length < length) {
              this.currentThankMarkdown = this.thanksMarkdown.substring(0, this.currentThankMarkdown.length + 1)
              let lastChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 1]
              let prevChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.thankEditor) {
                this.$nextTick(() => this.$refs.thankEditor.goBottom())
              }
              setTimeout(showThanks, interval)
            } else {
              resolve()
            }
          }
          showThanks()
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
    box-sizing: border-box;
  }
</style>
