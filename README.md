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