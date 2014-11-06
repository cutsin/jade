It's a W3C's spec: http://www.w3.org/html/wg/drafts/html/master/syntax.html#optional-tags

In browser, before HTML minify and after it, the result is different, because browser must be [generated implied end tags](http://www.w3.org/TR/html5/syntax.html#generate-implied-end-tags).

For Example, **[in this w3's essay](http://www.w3.org/People/Bos/CSS-variables) by Bert Bos, W3C/ERCIM, <bert@w3.org>**, he used  vast numbers of omitted tags.

If you using default option: true or  'safe', it's just provide 12 absolutely safe tags, most browsers(IE6+/chrome/safari/Firefox/Opera/...) works perfect.
Actually, it appeared in HTML 4.01, and we used many years on our corp's projects.

In test case, other levels will be fallback to "safe" when using "pretty: true", because it's really unsafe with space character and comment by [w3's SPEC](http://www.w3.org/html/wg/drafts/html/master/syntax.html#optional-tags).

Other features:
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