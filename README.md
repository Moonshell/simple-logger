# Simple Logger

> Version: 3.3

## 说明

移动端调试页面时的小工具，在页面最顶部的脚本前引用（`head`中也可），即可监听脚本中对于的`window.console`对象相关方法的调用，
将相关信息输出到页面内。通过点击屏幕上出现的黑色悬浮按键，即可呼出控制台信息记录进行查看。（悬浮按键可被拖动，以防调试时遮挡
页面元素）

实现了Chrome下`console`对象大部分方法的模拟，包括`log`, `warn`, `info`, `error`等，并可以使用`%`型的格式控制（可使用`%%`, `%c`, `%d`或`%i`, `%f`, `%s`, `%o`, `%O`）。

对浏览器全局错误事件也进行了监听，脚本出错时能跟踪到文件及代码行号，将相关错误信息通过`error`型信息输出到控制台供查看。

具体效果可参考`index.html`。

![效果图](https://github.com/Moonshell/simple-logger/blob/master/preview.png?raw=true)

## `SimpleLogger.tryCatch(callback)`

### `callback` : `Function` - 需要捕获的函数

特殊异常捕获。用于打包代码内，根据`sourcemap`分析具体的报错`stack`。

```javascript
    SimpleLogger.tryCatch(() => {
        throw new Error('Some error, maybe in bundled script.');
    });
```


## `SimpleLogger.hideBtn()`

隐藏日志操作按键，例子：

```html
<!DOCTYPE html>
<head>
    <meta charset="utf-8"/>
    <title>示例</title>
    <script src="js/simple-logger.js"></script>
    <script>
        if (window.location.host != 'testhost') {
            console.hideBtn();
        }
    </script>
```

（可作为防止发布正式环境时忘撤js文件的备选方案，当然，能做到的话，还是在正式环境的html中排除调试用的js文件比较好）

## 更新内容

### `3.3.1`

* 增加打包局部作用域下异常监听的 tryCatch 函数。


### `3.1.1`

* 完善对象字段内的 html 屏蔽。


### `3.1.0`

* 默认不允许输出 html，建议采用 border 的形式输出分割线。


### `3.0.8`

* 修复 Delayer.clearQueue 的问题


### `3.0.7`

* 修复移动端无法左右拖动问题。


### `3.0.6`

* 防止外部影响文本的对齐。


### `3.0.5`

* 修复滚动后点击误收起的问题。


### `3.0.1`

* 模块化重构，使用新的UI风格，支持object对象展开预览。


### `2.03`

* 修复字符串附加参数的多余引号问题。

