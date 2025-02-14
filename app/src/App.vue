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
let isPc = (function() {
    var userAgentInfo = navigator.userAgent;
    var Agents = ["Android", "iPhone",
        "SymbianOS", "Windows Phone",
        "iPad", "iPod"
    ];
    var flag = true;
    for (var v = 0; v < Agents.length; v++) {
        if (userAgentInfo.indexOf(Agents[v]) > 0) {
            flag = false;
            break;
        }
    }
    return flag;
}());
let getSecondsDiff = (startDate) => {
  const start = new Date(startDate.replace(/-/g, '/'));
  const now = new Date();
  const diff = now.getTime() - start.getTime();
  const totalSeconds = Math.floor(diff / 1000);

  const days = Math.floor(totalSeconds / (24 * 60 * 60));
  const hours = Math.floor((totalSeconds % (24 * 60 * 60)) / (60 * 60));
  const minutes = Math.floor((totalSeconds % (60 * 60)) / 60);
  const seconds = totalSeconds % 60;

  return {
    days: days,
    hours: hours,
    minutes: minutes,
    seconds: seconds,
    totalDays: Math.floor(totalSeconds / (24 * 60 * 60)),
    totalHours: Math.floor(totalSeconds / (60 * 60)),
    totalMinutes: Math.floor(totalSeconds / 60),
    totalSeconds: totalSeconds
  };
};

const startDate = '2025-01-31 23:07:00';
const secondsDiff = getSecondsDiff(startDate);
document.title += secondsDiff.totalSeconds + '秒';
export default {
    name: 'app',
    components: {
        StyleEditor,
        ResumeEditor
    },
    data() {
        return {
            interval: 27,
            currentStyle: '',
            enableHtml: false,
            fullStyle: [
                `/*
* Hi。宝！
* 我们的第一个情人节，希望给你一份特别的礼物。
*
* 聊了那么多，但程序员这个身份却太淡了！
* hh，这才是我的本职工作啊。
* 让我用代码，来为你写一封信，让网站留存我们的记忆^_^
* 嗯。说起来手机和电脑还得区分一下。
* 你现在用的是。。。${isPc ? '电脑' : '手机'}
*/

/* 首先给所有元素加上过渡效果 */
* {
  -webkit-transition: all .3s;
  transition: all .3s;
}
/* 白色背景太单调了。来点背景 */
html {
  color: rgb(222,222,222);
  background: rgb(0,43,54); 
}
/* 文字太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  ${ isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;' }
  font-size: 14px;
  line-height:1.5;
}
/* 这些代码颜色都一样。加点儿高亮区别来 */
.token.selector{ color: rgb(133,153,0) }
.token.property{ color: rgb(187,137,0) }
.token.punctuation{ color: yellow }
.token.function{ color: rgb(42,161,152) }
.token.comment{ color: rgb(177,177,177) }
/* 加个 3D 效果 */
html{
  -webkit-perspective: 1000px;
          perspective: 1000px;
}
.styleEditor {
  position: fixed; 
  ${ isPc ? 'left: 0;' : 'left:0;right:0;margin:auto;'}
  top: 0; 
  -webkit-transition: none; 
  transition: none;   
  ${ isPc ? '-webkit-transform: rotateY(10deg) translateZ(-100px) ;transform: rotateY(10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(-10deg) translateZ(-100px) ;transform: rotateX(-10deg) translateZ(-100px) ;' }
  ${ isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;' }
}

/* 再来一张信纸 */
.resumeEditor{
  position: fixed; 
  ${ isPc ? 'right: 0;' : 'left:0;right:0;margin:auto;'}
  ${ isPc ? 'top: 0;' : 'bottom:2%;'}
  padding: .5em;  
  ${ isPc ? 'margin: .5em;' : ''}
  ${ isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;' }
  border: 1px solid;
  color: #222;
  overflow: auto;
  font-size: 14px;
  line-height:1.5;
  background-size: cover;
  ${ isPc ? '-webkit-transform: rotateY(-10deg) translateZ(-100px) ;transform: rotateY(-10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(10deg) translateZ(-100px) ;transform: rotateX(10deg) translateZ(-100px) ;' }
    ${ isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;' }
  }
/* 我开始写了，看不清没事，一会我调整背景 */

`,
                `
/* 是不是看着很简陋粗糙？
 * 因为这是 Markdown 格式的
 * 一种程序员用来写文档日志的简易语言
 * 翻译成 网页 就行了
 * T T这个背景对眼睛不好，换成纯色
 */
`,
                `
/* 再加点样式 */
.resumeEditor {
  background: rgba(255,221,221,.9);
}
.resumeEditor{
  padding: 2em;
  line-height:1.8;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
  font-size:18px;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: rgba(221,221,221,.5);
}

/* OK。完成！ */

`
            ],
            currentMarkdown: '',
            fullMarkdown: `mxt × anran
----

2025-01-31 23:07:00，是你微信回复我的第一句话。  
in the moment，我们：  
\`相识 ${secondsDiff.totalDays} 天 ${secondsDiff.totalHours} 小时 ${secondsDiff.totalMinutes} 分钟 ${secondsDiff.totalSeconds} 秒\`  

相似家庭经历，相同的过年烦恼，不同的成长路线，却还是获得高度同频的思想和审美品位。  
物理上时间不长，精神上却感觉相识了无数个日夜。  
以往的时间里，听着相同音乐的我们，不同的时间，体会着相同的感动。  

## 1月31，第一次相识。  

## 2月03，第一次相见，一起唱歌。  
我们音乐品味是如此的高度一致，从没在任何人身上发生过，让我惊喜。  
晚饭的畅谈，我从你的眼神，你的回应，看到了共鸣。  

## 2月10，第一次牵你的手，一起逛艺术展。  
展会上，你说我什么都要点评两句，哈哈哈，行，好可爱。  
你说我审美不错，可以尝试练字，好开心收获王老师的认可。  
一起拿到了字帖，一起拍照，一起看了不知道在讲什么的视频，感觉好幸福。  
地铁上，想要拉住你的手，脑海却一片空白，我感到言语上的匮乏与笨拙。软软的，很小、纤细、美好，转瞬即逝。  
好快，不想结束，我想跟你下车。  

## 2月11日，第一次亲到你，一起看我的爱情观。  
这是我仅存的天真与烂漫，没有嘲笑或迎合，我看到你的思考与感受。  
剧情已经开始发散，一切变得朦胧与迷幻。在你耳边感受你的发香，脑海里飘荡起了王杰的:我是真的爱上你。  
我强装镇定，手汗出卖了我。  
片尾曲响起，放空，我感到精神上的交融，大脑告诉我，你的每一个点，终将变为我喜欢的优点，自我洗脑开始了。  
我变得笨拙，看着你，看窗外，悄悄变红的夜。  

## 暂别
瞬间，分隔两地，我感到无所适从。我尽力分享我的生活，为了精神上和你在一起，我也想了解你的生活。  
分享，使我们心的距离缩短。  
我开始患得患失。我更怕你了解我后，慢慢感到无趣，慢慢厌烦。  
仅仅是一天的分别，我感到不太对劲，一切都太快了，我无法集中注意力做想你之外的事。  
这样不像我，太冲动，缺少克制。吃下褪黑素，慢下来，mxt。  
醒来依旧，去跑步吧，但麻木的大脑没有变化。  
这时耳机里慵懒的旋律响起：呼吸决定，哈哈，怎么像是点我：“怎么那么坏，才两天就深爱，说的好像真爱”。  
我释怀了，让情绪决定，跟随呼吸心跳，快慢不由我的理性。  

----

“把丑事都说了出来，才会听我表白吧，我是真的喜欢你，真的，想谈恋爱了”，和我在一起吧。  


>【理解是最大的沟壑，但我拥有你，anran】  
>我来陪你走过余下岁月，共同经营，不离不弃。

`
        }
    },
    created() {
        this.makeResume()
    },

    methods: {
        makeResume: async function() {
            await this.progressivelyShowStyle(0)
            await this.progressivelyShowResume()
            await this.progressivelyShowStyle(1)
            await this.showHtml()
            await this.progressivelyShowStyle(2)
        },
        showHtml: function() {
            return new Promise((resolve, reject) => {
                this.enableHtml = true
                resolve()
            })
        },
        progressivelyShowStyle(n) {
            return new Promise((resolve, reject) => {
                let interval = this.interval
                let showStyle = (async function() {
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
    min-height: 100%;
}
.styleEditor {
    -webkit-backface-visibility: hidden;
}
</style>
