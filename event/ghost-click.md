# Ghost Click/点透
## 300ms触发等待时间
        大多数基于触摸的浏览器设备，在点击时都会有个 300ms 的事件触发等待时间。

        这个 300ms 为什么会被设计出来呢? 原因在于单击后面还有个双击缩放动作，这个涉及到触摸设备的手势交互行为原生设计，在平台提供商比如苹果和 google ,本意是通过 300ms 来区分两者之间的不同行为,单击一次等待 300ms 后没有再次单击那么就会触发缩放等双击行为。本意是好的,正常的逻辑实现,但是在现实的应用场景中,用户往往会觉得 web app 的事件触发不是那么灵敏,有那么一点延迟。
## Ghost Click/点透的来源
    由于为了解决300ms的延迟，很多人使用touchend模拟click事件（如zepto的tap事件）, [fastclick](https://github.com/ftlabs/fastclick)去解决。
    
    那么问题来了？
    当一旦触发了tap事件之后，被点击的对象隐藏切换之类（如：点击关闭对话框），那么300ms之后，click事件被触发，但是原本的对象已经被隐藏了,于是在那个坐标位置的元素被触发了click事件。Ghost Click/点透就是这样来了。
    
    
##解决方案
### DIV层阻挡(推荐方案)
* 用jQuery语法描述，其实原理就是用一个div阻挡原本的click事件

```javascript
    var $trick = $('<div/>')
        .appendTo('body')
        .css({
            'width' : '100%',
            'height' : '100%',
            'position' : 'absolute',
            'left' : 0,
            'top' : 0,
            'z-index' : 100000
        }).hide();
        
    //当发生tap点击之后
    $trick.show();
    //同时设置setTimeout
    setTimeout(function () {
        $trick.hide();
    }, 350)
```

### 停止冒泡


```javascript
    $('.button').on('touchstart click', function(e) {    
        e.stopPropagation(); //stops propagation
        if(e.type == "touchstart") {
            // Handle touchstart event.
        } else if(e.type == "click") {
            // Handle click event.
        }
    });
```


### 注意
    Chrome 开发团队不久前宣布，在 Chrome 32 这一版中，他们将[在包含 width=device-width 或者置为比 viewport 值更小的页面上禁用双击缩放]（https://codereview.chromium.org/18850005/）。当然，没有双击缩放就没有 300 毫秒点击延迟。