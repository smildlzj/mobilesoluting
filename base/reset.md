# HTML/CSS RESET
## Html
### 禁用Chrome自动翻译
```html
<meta name="google" value="notranslate">
```

### 点击无亮光
* windows phone需要在head添加
```html
<meta name="msapplication-tap-highlight" content="no">
```

* webkit需要在css添加
```css
-webkit-tap-highlight-color: rgba(0,0,0,0);
```

### 忽略页面中的数字识别为电话，忽略email识别
```html
<meta name="format-detection" content="telphone=no, email=no" />
```

### 禁止百度转码
```html
<meta http-equiv="Cache-Control" content="no-siteapp" />
```

### 关闭自动大写、拼写检查
```html
<input autocorrect="off" autocapitalize="off" spellcheck="false"/>
```

## CSS
### 去除IOS默认输入框样式
* [iOS forces rounded corners and glare on inputs](http://stackoverflow.com/questions/7599533/ios-forces-rounded-corners-and-glare-on-inputs)

```css
-webkit-appearance: none;
```

## 更多
* [HTML head 头标签](http://fex.baidu.com/blog/2014/10/html-head-tags/?utm_source=open-lib)