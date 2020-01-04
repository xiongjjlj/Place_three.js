# 问题：无法用GTLFLoader加载模型
我照着three.js的documentation做，到load model的时候，官方documentation这一步在这里，https://threejs.org/docs/index.html#manual/en/introduction/Loading-3D-models
文档里说的是有三种办法可以导入loader
>Loading
Only a few loaders (e.g. ObjectLoader) are included by default with three.js — others should be added to your page individually. Depending on your preference and comfort with build tools, choose one of the following:
```
// global script
<script src="GLTFLoader.js"></script>

// commonjs
var THREE = window.THREE = require('three');
require('three/examples/js/loaders/GLTFLoader');

// ES modules
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader';
```

但我自己尝试的时候，三种都分别有问题。

**1. 全局的，不太知道在js文件里去调用，这是我的代码**
```
<body>
    <script type='module' src="GLTFLoader.js">
        var loader = new GLTFLoader();

        loader.load('./model/hopson2Fgltf.gltf', function(gltf){

            scene.add( gltf.scene );

        }, undefined, function ( error ) {

            console.error( error );

        } );
    </script>
</body>
```
报错是这样
`Access to script at 'file:///C:/Computer/Document/Professional/Place.int/hopson/Coding/GLTFLoader.js' from origin 'null' has been blocked by CORS policy: Cross origin requests are only supported for protocol schemes: http, data, chrome, chrome-extension, https. [file:///C:/Computer/Document/Professional/Place.int/hopson/Coding/index.html]
Failed to load resource: net::ERR_FAILED [file:///C:/Computer/Document/Professional/Place.int/hopson/Coding/GLTFLoader.js]`

**2. require那种，主要问题是require is not defined，我尝试了网上的bundle方法还是没有解决，要什么样的情况才能用require？**

**3. 报错跟第一个一样**
```
<body>
    <script type='module'>
        import { GLTFLoader } from './node_modules\three/examples/jsm/loaders/GLTFLoader';

        var loader = new GLTFLoader();

        loader.load('./model/hopson2Fgltf.gltf', function(gltf){

            scene.add( gltf.scene );

        }, undefined, function ( error ) {

            console.error( error );

        } );
    </script>
</body> 
```

## 关于1和3的报错，我查了下说是跨域问题，不知道有没有服务器的问题？是不是浏览器打不开外部文件之类的？（网上写的太复杂已经无法理解了- -）关于2的报错，怎么才能用那个require？网上很多方法我都试过,说是要打包资源，如果要用browserify打包，是应该怎么打包？
# 感谢！
