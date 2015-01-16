# 可省略标签的[Jade](https://github.com/jadejs/jade)

首先，这是个W3规范：http://www.w3.org/html/wg/drafts/html/master/syntax.html#optional-tags


## 安装

npm install cutsin/jade


## 使用

```bash
bash$ jade foo bar --omitTag [safe|redical|unsafe|dangerous]
```
```javascript
var jade = require('jade')
var options = {
	omitTag : 'redical'	// or 'safe' or 'unsafe' or 'dangerous'
}
var fn = jade.compileFile('./foo.jade', options)
var html = fn(locals)
```


## 为什么要省略标签？

1. 文一：[《为什么要省略html标签》](https://github.com/cutsin/Passion-of-the-Cutsin/blob/master/2013/03/%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E7%9C%81%E7%95%A5html%E6%A0%87%E7%AD%BE.md)

2. 文二：[《可省略的html标签及其实践》](http://moonless.net/demo/optional-tags/)

3. 在浏览器中，HTML在压缩（去掉空白字符）前后，渲染的结果是不同的，因为浏览器会[按照规范生成隐式结束标记](http://www.w3.org/TR/html5/syntax.html#generate-implied-end-tags)。

4. CSS两位创始人之一的Bert Bos, W3C/ERCIM, <bert@w3.org>在一篇著名论文[《Why CSS variables are harmful》（为什么“变量”在CSS中是有害的）](http://moonless.net/demo/CSS-variables/)中全程使用了省略标签。

5. 根据[omitted tag's implicit rules](http://www.w3.org/TR/html5/syntax.html#generate-implied-end-tags)，可以做很多有用的事情。比如对于Jade，可以减少缩进层级：

__至少需要`omitTag: 'radical'`__
```jade
doctype html
html(lang="zh-CN")
//- 由于base只能出现在head里，用它作为head/body分界
base(href="/n")
p 正文
ul
  li
```


## 这安全吗？

1. 完全跟Jade同步，只是作了少量改动。
2. 如果使用默认选项：`omitTag: true|'safe'`，只省略了12个绝对安全的标签，在绝大多数浏览器（IE6+/chrome/safari/Firefox/Opera/...）中都能完美工作。
3. 实际上，它在HTML 4.01规范中就已经出现，而且在很多大型项目中已应用了很多年。
4. 在测试用例中可以看到，如果你同时开启了`pretty: true`，会自动回滚为`omitTag: 'safe'`，因为在包含空白字符和注释的情况下，的确有[一些不安全的情况（w3's SPEC](http://www.w3.org/html/wg/drafts/html/master/syntax.html#optional-tags)）。

## License

[MIT](LICENSE)