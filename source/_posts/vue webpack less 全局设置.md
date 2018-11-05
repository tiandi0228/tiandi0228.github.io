---
layout: vue
title: vue webpack less 全局设置
date: 2018-05-09 20:49:08
tags: 
- vue 
- webpack 
- less 
- main
---

今天打算在一个新项目中使用less，但是在使用中发现定义在全局文件common.less中的变量，不能在单独的vue中使用。下面是解决的方法：
```
npm install sass-resources-loader --save-dev
```

找到 build/utils.js，在 function generateLoaders(loader, loaderOptions) { 上面插入下面这段
```
function resolveResource(name) {
    return path.resolve(__dirname, '../src/assets/less/' + name);
}

// 解决不能全局引用less变量问题
function generateSassResourceLoader() {
    var loaders = [
        cssLoader, 
        'less-loader',
        {
            loader: 'sass-resources-loader',
            options: {
                // it need a absolute path  
                resources: [resolveResource('common.less')]
            }
        }
    ];
    if (options.extract) {
        return ExtractTextPlugin.extract({
            use: loaders,
            fallback: 'vue-style-loader'
        })
    } else {
        return ['vue-style-loader'].concat(loaders)
    }
}
```

继续修改：
```
less: generateLoaders(),
替换成
less: generateSassResourceLoader(),
```