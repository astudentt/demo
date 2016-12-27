# 开发登录页面有感
刚过完圣诞节，但是登录页面还是没有更版。其中涉及很多第一次遇到的问题，所以使开发过程变得缓慢，
经历了如此惨绝人寰的开发过程，所以决定总结出涉及的关键点，方便其他的朋友们开发借鉴。先从简单
地样式写起.


####1.placeholder样式设置


  *placeholder* 已经是大家常用的属性了，在移动端的开发是十分常见的。如果你想要让你的placeholder和input框内容的样式不同，你只需要为placeholder设置自己的样式即可，代码如下：

>::-moz-placeholder {
    color: #cccccc;
    font-size:16px;
}
:-ms-input-placeholder {
    color: #cccccc;
    font-size:16px;
}
::-webkit-input-placeholder {
    color: #cccccc;
    font-size:16px;
}

> ######实现效果如下：

![signin](path/image/signin1.png "登录")
