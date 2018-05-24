# demo-douban

> A Vue.js project built with vue-cli, vue-router and vuex.

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```


## Douban API

[Movie API Doc](https://developers.douban.com/wiki/?title=movie_v2)

* 正在热映 GET https://api.douban.com/v2/movie/in_theaters
* 即将上映 GET https://api.douban.com/v2/movie/coming_soon 
* Top 250 GET https://api.douban.com/v2/movie/top250 

由于豆瓣api的跨域问题，不能直接通过ajax请求访问。考虑到只涉及到GET请求，这里使用了第三方库[jsonp](https://www.npmjs.com/package/jsonp)进行HTTP请求。
本地开发环境还可以使用vue-cli的[代理配置](http://vuejs-templates.github.io/webpack/)


## 遇到的困难

1. Vuex的getters接受参数问题

getters只接受默认参数state,其他getters，不能随意传入参数。
需要使用高阶函数，返回的函数接受用户的参数(id)。
见vuex官方demo https://vuex.vuejs.org/getters.html

``` javascript
getLocalId: (state, getters) => (id) => {
    if(state.localData.indexOf(id) > 1) {
        return state.localData.indexOf(id);
    } else {
        return -1;
    }
}
```