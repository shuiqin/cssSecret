# cssSecret
#简介
####由于水平有限，编写的过程难免会有诸多错误，也希望大家在看的过程中发现了问题，可以在 Github 上给该项目发 Pull Request。衷心希望可以有更多的人参与到本书的编写当中

##检测某个样式属性是否被支持 思路: 任一元素的element.style上是否有该属性
`
var root = document.documentElement; // <html>
if ('textShadow' in root.style) { root.classList.add('textshadow');
} else {
    root.classList.add('no-textshadow');
}
`

