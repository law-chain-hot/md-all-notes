# NPM, Babel, Webpack
> The old version
- The difference
    - devDependency
    - Dependency
        - The first one is for dev period
- .ignore
    - $ touch ignore
    - 直接输入文件名/
- Babel新版本用@babel/env语法 （babel-env以前是这样）
- Webpack -> to integrate other file together



---
# The New Part
## How to use Babel
1. install package, and add the module/rule
2. **`creat a config file`**, .babelrc
3. put the **babel-polyfill** into entry



## MVC
![image](https://user-images.githubusercontent.com/57960778/69845223-7a247e00-1235-11ea-92fe-38adc44cc5b6.png)

Model-View-Controller



## Three different ways to import
You can choose each way you like
```js
import str from './model/Search';
// import { sum as s, multiply as m, ID } from './view/searchView';
import * as search from './view/searchView';

console.log(`Using imported function, ${search.sum(search.ID, 3)}, and multiply ${search.multiply(3,5)}, ${str}`);
```



## Axios
From Vue's author
And this is Search method, which should be put into `Model/Search.js` as a class `Search`
```js
import axios from 'axios';

async function getResult(query) {
    const proxy = 'https://cors-anywhere.herokuapp.com/';
    try{
        const res = await axios(`https://forkify-api.herokuapp.com/api/search?&q=${query}`);
        const recipes = res.data.recipes;
        console.log(res);
        console.log(recipes);
    } catch (error){
        alert(error);
    }
```


## 建立Search Controller
### 建立class Search
包括里面的function `async getResult()`


### Q&A
为什么是`submit`在`addEventListener`?
-不知道。。。
```js
document.querySelector('.search').addEventListener('submit', e => {
    e.preventDefault(); //阻止点了button后，页面reload
    controlSearch();
});
```


## 建立Search View
在`view`文件下建立`base.js`, 储存所有DOM到`elements, 使用下面这个命令把elements引入到所有地方
```js
import { elements } from "./base";
```
```js
// **痛苦的Debug**
arrow function ( ) => { } 只有在没有curly brace{}时，才自动返回only 1 line
```

### searchInput( )
Get the `input` from the UI, and convert this `input` into Search controller


### renderResults( )
1. 接着render每个recipe, 写成单独的`renderRecipe` 
2. `renderResults` -> forEach -> `renderRecipe`
3. 在`renderRecipe`里面用 `markup` 代表HTML内容接着使用 
`elements.searchResList.insertAdjacentHTML('beforeend', markup);`
```js
// **痛苦的Debug**
卧槽,记得 querySelector(.class) 选class的时候,一定要用copy,一字之差都
不不行, //亚麻色头发的少女
```

### clearPart( )
最后插入2个clear function, 分别清空`input`和`result`


### const limitRecipeTitle = (title, limit = 17) => { }
没意思, 把长于17个字母的菜名后面的变为..., 我会在water flow里面忽略它
另外 private 函数就是`非export`的函数


### 转到view/base.js
建立 `export const renderLoder`, 实现在await的时候加载loader动画, 找到`class = parent`, 然后使用把loader的代码插入HTML中
```js
parent.insertAdjacentHTML('afterbegin', loader); 
```
最后clearLoader, 记得用 **loader.parentNode.removeChild(loader)**, 不然会留下一个空间


### renderButton( )
更新 renderResults( ), 让其显示部分结果在一页, by recipes.slice.(srt, end).forEach( )
其中 creatButton( )中有个新元素很重要, **data-togo=${newPage}** 用于 even delegation 时捕捉页码
```js
//creatButton( )
    let markup = `<button class="btn-inline results__btn--${type}" data-togo=${newPage} > `;
    // data-togo!
```
接着在 btn 上加上 event, 使用 event delegation去操作, 最后再clear result, 同时 clear 老的button
```js
elements.searchResPages.addEventListener('click', e => {
    const btn = e.target.closest('.btn-inline');
    if (btn) {
        const goToPage = parseInt(btn.dataset.goto, 10); // ????????!!!!!!   dataset, 10
        searchView.clearRes();
        searchView.renderResults(state.search.result, goToPage);
    }
});
```

console.log(btn.dataset);
```js
// DOMStringMap {goto: "3"}
// goto: "3"
// __proto__: DOMStringMap
```

```js
// **痛苦的Debug**
上面的data-goto, 我写成了data-togo
```







---
---
---
# Water Flow
>**[模块M]** 首先建立 **`Model/Search.js`** 里面的class `Search` 

>**[模块C]** 建立 **`Search Controller`**，async 函数，5个步骤

1. get query from view `实现得到Input, 在view里面实现`
2. new search obj and add to state `不是很懂为什么要new一个state`
3. prepare UI for results `实现loader, clear等, 在view里面实现`
4. search for recipes `实现返回菜单`
5. render the result on UI `实现recipe部署, 在view里面实现`

>**[模块V]** 建立 **`Search View`** 

1. searchInput( ) `实现Input输入`
2. renderResults( ) -> forEach -> 通过renderRecipe( ) `实现recipe的部署`
3. clearPart( ) `清空面板为下一次search`
4. limitRecipeTitle ( ) `实现长字符多余的部分变为...`
5. renderLoder( ) `实现loader动画效果(包括出现和clear)`
6. renderButton( ) `实现分页效果pagination, 接着再把其insert到html`
7. creatButton( ) `实现return markup`

>**[模块C]** 建立 **`Event Delegation`** for `page button`

- 翻页时鼠标点击的 Event, 匹配到 target 然后用 closest 找到整个 btn, 从 btn 里面得到page-goto的信息






