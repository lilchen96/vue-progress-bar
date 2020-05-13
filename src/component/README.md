## vue-circular-progress

基于 Vue 的环形进度条

#### 使用说明

1.安装
`npm install illmatic-progress-bar --save`

or

`yarn add illmatic-progress-bar`

2.注册：
`import illmaticCircularProgress from 'illmatic-progress-bar';`

`Vue.use(illmaticProgressBar);`

3.使用
`<illmatic-progress-bar></illmatic-progress-bar>`

#### 参数

##### props:

styleOptions:{
&nbsp;&nbsp;&nbsp;&nbsp;height: 10,&nbsp;&nbsp;// 进度条高度
&nbsp;&nbsp;&nbsp;&nbsp;progressColor: "#87CEFA",&nbsp;&nbsp;// 进度条颜色
&nbsp;&nbsp;&nbsp;&nbsp;backgroundColor: "#EDEDED"&nbsp;&nbsp;// 进度条底色
}

direction: "clockwise"&nbsp;&nbsp;//进度条方向（顺时针：clockwise，逆时针：anticlockwise）

duration: 100&nbsp;&nbsp;// 总量（例如：100S）

progress: 40&nbsp;&nbsp;// 当前进度（例如：40S）

autoPlay: true&nbsp;&nbsp;//进度条是否自动播放

##### methods:

run()&nbsp;&nbsp;//进度条开始

stop()&nbsp;&nbsp;//进度条暂停

reset()&nbsp;&nbsp;//进度条重置
