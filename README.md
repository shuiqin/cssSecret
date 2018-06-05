# cssSecret
# 简介

### 由于水平有限，编写的过程难免会有诸多错误，也希望大家在看的过程中发现了问题，可以在 Github 上给该项目发 Pull Request。衷心希望可以有更多的人参与到本书的编写当中

## 检测原理
如果要检测选择符和 @ 规则的支持情况,则会稍稍复杂一些。不过原 理也很简单,在解析 CSS 代码时,浏览器总会丢弃它自己无法识别的部分, 
因此我们可以动态地应用样式并检查它是否生效,以此来判断浏览器是否可 以识别某个特性。
当然,我们也要清楚地认识到,浏览器可以解析某个 CSS 特性并不代表它已经实现(或正确实现)了这个特性。
### 检测某个样式`属性`是否被支持 思路: 任一元素的element.style上是否有该属性
```javascript
var root = document.documentElement; // <html>
if ('textShadow' in root.style) { 
    root.classList.add('textshadow');
} else {
    root.classList.add('no-textshadow');
}

function testProperty(property) {
    var root = document.documentElement;
    if (property in root.style) {
        root.classList.add(property.toLowerCase()); 
        return true;
    }
    root.classList.add('no-' + property.toLowerCase());
    return false; 
}
```

### 检测某个`具体属性值`是否支持 把值赋给某个对应的属性, 然后检查浏览器是否海保存这个值
```javascript
function testValue(id, value, property) { 
    var dummy = document.createElement('p'); 
    var root = document.documentElement; //p29 issues
    dummy.style[property] = value;
     if (dummy.style[property]) { 
        root.classList.add(id); 
        return true;
     }
     root.classList.add('no-' + id);
     return false; 
     }
```

## CSS3规范
 * CSS [语法](http://w3.org/TR/css-syntax-3)
 * CSS [层叠与继承](http://w3.org/TR/css-cascade-3)
 * CSS [颜色](http://w3.org/TR/css3-color)
 * [选择符](http://w3.org/TR/selectors)
 * CSS [背景与边框](http://w3.org/TR/css3-background) 
 * CSS [值与单位](http://w3.org/TR/css-values-3)
 * CSS [文本排版](http://w3.org/TR/css-text-3)
 * CSS [文本装饰效果](http://w3.org/TR/css-text-decor-3) 
 * CSS [字体](http://w3.org/TR/css3-fonts)
 * CSS [基本 UI 特性](http://w3.org/TR/css3-ui)
 此外,如果某个模块是前所未有的新概念,那它的版本号将从 1 开始。 比如下面这些:
 * CSS [变形](http://w3.org/TR/css-transforms-1)
 * [图像混合效果](http://w3.org/TR/compositing-1) 
 * [滤镜效果](http://w3.org/TR/filter-effects-1)
 * CSS [遮罩](http://w3.org/TR/css-masking-1)
 * CSS [伸缩盒布局](http://w3.org/TR/css-flexbox-1) 
 * CSS 网格布局(http://w3.org/TR/css-grid-1)
 尽管“CSS3”这个名词非常流行,但它实际上并没有在任何规范中定 义过。这一点跟 CSS 2.1 或更早的 CSS 1 不一样。真正的情况是,绝大多
 
 ### 灵活的按钮
 * 按钮1
 ```
 padding: .3em .8em;
 border: 1px solid #446d88;
 background: #58a linear-gradient(#77a0bb, #58a); 
 border-radius: .2em;
 box-shadow: 0 .05em .25em gray;
 color: white;
 text-shadow: 0 -.05em .05em #335166;
 font-size: 125%;
 line-height: 1.5;
 ```
 缺点: 要根据按钮的亮面和暗面相对于主色调   #58a 变亮和变暗的程度来分别推 导出其他颜色各自的亮色和暗色版本。
 此外,若我们想把按钮放在一个非白 色的背景之上呢?显然使用灰色( gray)作投影只适用于纯白背景的情 况。
 
 *改良的灵活的按钮
 **半透明的黑色或白色叠加在主色调上,即可产生主色调的亮 色和暗色变体,**
 // 推 荐 使 用 HSLA 而 不 是 RGBA 来产生半透明的白色,因 为它的字符长度更短,敲起来也 更快。这归功于它的重复度更低
 ```
 padding: .3em .8em;
 border: 1px solid rgba(0,0,0,.1);
 background: #58a linear-gradient(hsla(0,0%,100%,.2),
                                  transparent);
 border-radius: .2em;
 box-shadow: 0 .05em .25em rgba(0,0,0,.5); 
 color: white;
 text-shadow: 0 -.05em .05em rgba(0,0,0,.5);
 font-size: 125%; 
 line-height: 1.5;
 
 
 button.cancel { background-color: #c00;
 }
 button.ok { background-color: #6b0;
 }
 ```
 
 ### baseline理解 vertical-align默认是基线对齐
  参考 (https://www.cnblogs.com/xuhaodong/p/basseline.html)
  
 ### 代码易维护(改动尽可能少)
 ```
 border-width: 10px 10px 10px 0;
 ```
 使用下面的代码 border-width变啦只需改一个地方
 ``` 
 border:10px
 border-left-width:0px
 ```
 
 ###  currentColor  css史上第一个变量
 未来,我们在原生 CSS 中拥有处理颜色的函数后,currentColor 就会 变得更加有用,因为我们可以用这些函数来产生其各种深浅明暗的变体。

 ### 提示框上的倒三角
 ```
  .callout:before{
             content: "";
             position: absolute;
             top: -.45em;
             left: 1em;
             padding: 0.35em;
             background: inherit;
             border: inherit;
             border-right: 0;
             border-bottom: 0;
             transform: rotate(45deg);
         }
 ```
 
 ### 视觉上的错觉 p42
 * 对完美垂直居中的布局看着偏上
 * 同宽同高的圆比 正方形看着小
 * 文字边距设一样 上下看着边距比左右更大
 
 ### 媒体查询的断点不应该🈶️具体的设备来决定 应根据设计自身决定
 及pc端以任意尺寸的窗口来显示都能很好的显示
     *使用百分比或视口相关的单位(视口宽度或高度的百分比) (vw vh vmin vmax) 
     [参考](https://blog.csdn.net/ZNYSYS520/article/details/76053961)