# clamp

[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

[Demo](https://jingchaofang.github.io/clamp.js/examples/demo.html)

## 其它库

[vue-clamp](https://github.com/Justineo/vue-clamp)

## 开发

```
npm run build
npm run start
npm run eslint
./benchmark/test.html
```

## css截取应用

限制2行打点

```css
.clamp {
    text-overflow: ellipsis;
    overflow: hidden;
    display: -webkit-box;
    -webkit-box-orient: vertical;
}
.clamp2 {
    -webkit-line-clamp: 2;
}
```

限制1行打点`-webkit-line-clamp:1`

```css
.clamp {
    text-overflow: ellipsis;
    overflow: hidden;
    display: -webkit-box;
    -webkit-box-orient: vertical;
}
.clamp1 {
    -webkit-line-clamp: 1;
}
```

限制1行打点

```css
.ellipsis {
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
}
```

后跟元素限制1行打点

```css

／*元素紧跟*／
.ellipsis-auto {
  display: inline-block;
  width: auto;
  max-width: 100%;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

／*元素贴右*／
.ellipsis-full {
  display: inline-block;
  width: 100%;
  max-width: 100%;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
```


## js截取应用

包裹元素不定高`clamp.zepto.js`截取并拼接片段，不定高容易出现大幅度闪动，影响体验

```js
var $intro1 = $('#intro1');
var clampResult1 = $intro1.clamp({
    clamp: 3,
    truncationHTML: '...'
});
```

包裹元素定高`clamp.zepto.js`截取并拼接片段，定高防止大幅度闪动，但是追加的片段折叠按钮会闪动

```js
var $intro2 = $('#intro2');
var clampResult2 = $intro2.clamp({
    hasHeight: true,
    truncationHTML: '...'
});
```

包裹元素定高并且有内容标签逻辑限制是否有折叠按钮`clamp.zepto.js`截取并拼接片段，没有传参force，会忽略一种追加片段的情况：文本不够截取时，内容标签有隐藏内容时

```js
    var $tag3 = $('#tag3');
    var $intro3 = $('#intro3');
    var clampResult3 = $intro3.clamp({
        hasHeight: true,
        truncationHTML: '...'
    });

    if ($intro3.data('clamp') || $tag3.get(0).scrollHeight > $tag3.get(0).clientHeight) {
        $intro3.on('click', function() {
            if($(this).data('clamp')) {
                $intro3.html(clampResult3.original + '...');
                $intro3.css({ 'height': 'auto' });
                $tag3.css({ 'height': 'auto' });
                $(this).data('clamp', false);
            } else {
                $intro3.html(clampResult3.clamped);
                $intro3.css({ 'height': '' });
                $tag3.css({ 'height': '' });
                $(this).data('clamp', true);
            }
        });
    }
```

包裹元素定高并且有内容标签逻辑限制是否有折叠按钮`clamp.zepto.js`截取并拼接片段，force判断是否强制添加折叠按钮

```js
/**
 * 标签有隐藏内容
 */
var $tag4 = $('#tag4');
var $intro4 = $('#intro4');
var clampResult4 = $intro4.clamp({
    hasHeight: true,
    truncationHTML: '...',
    force: $tag4.get(0).scrollHeight > $tag4.get(0).clientHeight ? true : false
});

if ($intro4.data('clamp') || $tag4.get(0).scrollHeight > $tag4.get(0).clientHeight) {
    $intro4.on('click', function() {
        if ($(this).data('clamp')) {
            $intro4.html(clampResult4.original + '...');
            $intro4.css({ 'height': 'auto' });
            $tag4.css({ 'height': 'auto' });
            $(this).data('clamp', false);
        } else {
            $intro4.html(clampResult4.clamped);
            $intro4.css({ 'height': '' });
            $tag4.css({ 'height': '' });
            $(this).data('clamp', true);
        }
    });
}
```

```js
/**
 * 标签有隐藏内容
 */
var $tag5 = $('#tag5');
var $intro5 = $('#intro5');
var clampResult5 = $intro5.clamp({
    hasHeight: true,
    truncationHTML: '...<span class="triangle down"></span>',
    force: $tag5.get(0).scrollHeight > $tag5.get(0).clientHeight ? true : false
});
if ($intro5.data('clamp') || $tag5.get(0).scrollHeight > $tag5.get(0).clientHeight) {
    $intro5.on('click', function() {
        if ($(this).data('clamp')) {
            $intro5.html(clampResult5.original + '<span class="triangle up"></span>');
            $intro5.css({ 'height': 'auto' });
            $tag5.css({ 'height': 'auto' });
            $(this).data('clamp', false);
        } else {
            $intro5.html(clampResult5.clamped);
            $intro5.css({ 'height': '' });
            $tag5.css({ 'height': '' });
            $(this).data('clamp', true);
        }
    });
}
```

```js
/**
 * 对多个元素文本截取
 */
var $intros = $('.intros');
for (var i = 0; i < $intros.length; i++) {
    $intros.eq(i).clamp({
        hasHeight: true,
        truncationHTML: '...<span class="triangle down"></span>'
    });
}
```
