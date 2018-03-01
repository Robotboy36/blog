
### 一、简介
```
livescript于95年诞生于Netscape公司(Gecko引擎创建团队,98年被收购,07年正式退出浏览器大战)，
与sun公司合作，为蹭java热点，命名为javascript。
微软则推出针对IE的JScript与其竞争, ScriptEase也推出CEnvi, 各自为营。
97年，ECMA(欧洲计算机制造商协会)出面干涉，制定脚本语言的标准规范，ECMAScript，
随后的版本都以该规范命名。
ECMAScript 3, ECMAScript 5, 
ECMAScript 2015(es6), ECMAScript 2016(es7), ECMAScript 2017(es8)

如今，js成为一种高频使用的编程语言，也越发成熟， 前端工程师不再是写写页面效果，
更多关注项目构建，性能优化，可扩展性，健壮性；使用面向对象，模块化，组件化，
mvc等编程思想。涉及业务功能也涵盖金融，游戏，在线教育，视频直播，VR，App等等。
```

### 二、js的使用
- #### 在页面中使用script
``` html
    <html>
        <head>
            <script>
                // script 代码
                // 不用加 type="text/javascript" 属性， 默认type即是这个
            </script>
        </head>
        <body>
            <div></div>
            
            <script>
                // script标签可以放在任意地方
                // 但是通常我们建议放在body的最底部
                // 因为页面的加载顺序关系(后面章节详细说)，网页会先加载head, 然后是解析body的dom结构
                // 如果我们在js中操作了dom， 就需要在浏览器解析dom后执行
            </script>
        </body>
    </html>
```

- #### 使用外部script文件，在页面中引入
``` html
    <html>
        <head>
            <!-- 
                引入路径说明

                /: 根路径
                ./: 当前路径
                ../: 当前路径的父节点路径
                ../../: ../ 类推..
                http://www.baidu.com/a.js: 网络路径，通常用在cdn资源上
             -->
            <script src="./a.js"></script>
            <script src="http://www.baidu.com/a.js"></script>
        </head>
        <body>
            <div></div>
            
            <!-- 
                引入外部文件的方式可以使得代码结构更加清晰，方便复用
                也方便小伙伴之间分工合作，
                但是也会增加一个http请求，通常我们还是会使用独立文件，因为代码是可以使用构建工具合并的
             -->
            <script src="http://www.baidu.com/b.js"></script>
        </body>
    </html>
```

- #### 使用时需要注意的点
    由于网页的解析是从上往下，如果引入多个js，并且js中有相同的全局变量或方法，后面会覆盖前面的
    

- #### 优化方案
``` html
    <script src="./a.js" defer>
    <script src="./a.js" async>

    由于js在下载过程中会阻塞后面资源的加载， 所以js给出两个属性用来设置脚本的下载和执行方式
    defer: 延迟下载脚本，排在下载资源队列的后面，下载完立即执行
    async: 正常下载，但不阻塞后面资源的下载，下载完立即执行

    注意事项：
    1、需要在body解析dom之前的js不适合用defer属性，比如 html5shim
    2、有依赖关系的js之间不适合用async属性, 比如b.js必须依赖jq运行，
    则jq必须先于b.js加载执行，因为async表示异步加载，加载顺序是不固定的，
    所以需要注意这点
```