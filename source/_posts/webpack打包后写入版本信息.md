---
title: webpack打包后写入自定义信息
date: 2020-03-06 22:45:20
tags: 
- webpack
- plugins
- fs
---
今天因项目需要做版本管理，在使用webpack打包后的需要从package.json获取到的信息写入到打包生成的js文件里，所以做了一下研究，以此来记录。

首先来创建一个config-webpack-plugin.js插件：
````
'use strict';
/**
 * 向打包后的文件写入信息
 */
const fs = require('fs');
const packageInfo = require('./package.json');

class ConfigWebpackPlugin {
    // 在构造函数中获取用户给该插件传入的配置
    constructor(options) {
    }
    
    // Webpack 会调用 ConfigWebpackPlugin 实例的 apply 方法给插件实例传入 compiler 对象
    apply(compiler) {
        // done: 该事件在成功构建并且输出了文件后，Webpack 即将退出时发生;
        compiler.plugin('done', _ => {
            const msg = `/* Version: ${packageInfo.version} Author:  ${packageInfo.author} */`;
            const data = fs.readFileSync('./lib/index.js', 'utf8').split('');
            data.splice(0, 0, msg);
            fs.writeFileSync('./lib/index.js', data.join(''), 'utf8');
        });
    }
}

module.exports = ConfigWebpackPlugin;
````

在webpack.config.js的plugins数组中，添加一个插件的实例:
````
const ConfigWebpackPlugin = require('./config-webpack-plugin');

module.exports = {
    plugins:[
        new ConfigWebpackPlugin()
    ]
}
````
最后就可以在打包生成的文件的头部看到写入的自定义信息了。
