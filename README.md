# [Jade](https://github.com/jadejs/jade) with optional tags

[中文文档](README.zh-CN.md)

It's a W3C's spec: http://www.w3.org/html/wg/drafts/html/master/syntax.html#optional-tags

## Usage

```bash
bash$ jade foo bar --omitTag [safe|radical|unsafe|dangerous]
```
```javascript
var jade = require('jade')
var options = {
	omitTag : 'radical'	// or 'safe' or 'unsafe' or 'dangerous'
}
var fn = jade.compileFile('./foo.jade', options)
var html = fn(locals)
```


## Why?

1. [Why we need optional tags](https://github.com/cutsin/Passion-of-the-Cutsin/blob/master/2013/03/%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E7%9C%81%E7%95%A5html%E6%A0%87%E7%AD%BE.md)

2. http://moonless.net/demo/optional-tags/

3. In browser, before HTML minify and after it, the result is different, because browser must be [generated implied end tags](http://www.w3.org/TR/html5/syntax.html#generate-implied-end-tags).

4. **[In this w3's essay](http://www.w3.org/People/Bos/CSS-variables) by Bert Bos, W3C/ERCIM, <bert@w3.org>**, he used  vast numbers of omitted tags.


## It's really safe?

1. Sync with Jade, only a few changes.

2. If you using default option: true or  'safe', it's just provide 12 absolutely safe tags, most browsers(IE6+/chrome/safari/Firefox/Opera/...) works perfect.

3. Actually, it appeared in HTML 4.01, and we used many years on our corp's projects.

4. In test case, other levels will be fallback to "safe" when using "pretty: true", because it's really unsafe with space character and comment by [w3's SPEC](http://www.w3.org/html/wg/drafts/html/master/syntax.html#optional-tags).

## Other features

- Optimize transfer: 
- Improve performance: 
- Make easier to handle [white-space processing model](http://www.w3.org/TR/2013/WD-css-text-3-20131010/#white-space-rules)
- Doesn't affect the performance of the browser

```html
<style>
.a li {display:block}
.b1 li {display:inline-block}
.b2 li {display:inline}
</style>
<ul class="a">
  <li>Hi~</li>
  <li>ForbesLindesay</li>
</ul>
<ul class="b1">
  <li>Hi~
  <li>ForbesLindesay
</ul>
<ul class="b2">
  <li>Hi~
  <li>ForbesLindesay
</ul>
```
In browser, the rendering results are different, because of [white-space processing model](http://www.w3.org/TR/2013/WD-css-text-3-20131010/#white-space-rules)

In addition, according to [omitted tag's implicit rules](http://www.w3.org/TR/html5/syntax.html#generate-implied-end-tags), we can do a lot of useful things.


Values for Jade, it can be reduce indentationslike this:

__Must be: `omitTag: 'radical'` at least__
```jade
doctype html
html(lang="en")
//- `base` is a `head scope` only tag.
base(href="/n/contacts/")
p I'm main body.
ul
  li
```
It can resolve the different rendering results on browser side([white-space processing model](http://www.w3.org/TR/2013/WD-css-text-3-20131010/#white-space-rules)) when using `pretty: true`

## License

[MIT](LICENSE)