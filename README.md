# 开发登录页面有感
刚过完圣诞节，但是登录页面还是没有更版。其中涉及很多第一次遇到的问题，所以使开发过程变得缓慢，
经历了如此惨绝人寰的开发过程，所以决定总结出涉及的关键点，方便其他的朋友们开发借鉴。先从简单
地样式写起.


####1.placeholder样式设置


  *placeholder* 已经是大家常用的属性了，在移动端的开发是十分常见的。如果你想要让你的placeholder和input框内容的样式不同，你只需要为placeholder设置自己的样式即可，代码如下：


> ::-moz-placeholder {

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

######实现效果如下：

<img  src='image/signin1.png'>

<img  src='image/sign2.png'>

####blur事件与click事件冲突

如图，一键清除按钮点击之后需要清除文本框内容，并且在文本框失去焦点时需要将一键清除按钮隐藏。这需要在两个事件添加实现代码，input的blur事件，以及btn的click事件

<img  src='image/signIn3.png'>

> $(".input'").blur(function() {

    $(".btn").hide(); //隐藏一键清除按钮
  
});
  
  $(".btn").click(function() {
   
    $('.input').val(""); //清除input框内容
     
     $('.input').focus(); //input框获取焦点

});

但是在测试的过程中发现click事件不被触发，后来查了些资料并且做了测试，发现blur事件哥click事件会有冲突，所以只要为blur事件添加setTimeout函数，在固定秒数后执行即可。修改后的代码为：

> $(".input'").blur(function() {    
    
    setTimeout(function () {

      $(".btn").hide(); //隐藏一键清除按钮
    
    }, 300);  
  });
  
  $(".btn").click(function() {
    
    $('.input').val(""); //清除input框内容
     
     $('.input').focus(); //input框获取焦点

});

####ajax内部添加onfocus事件在异步情况下不起作用

点击获取验证码后需要调取ajax并通过返回值判断是否下发成功如果下发成功，则将验证码文本框设为可用状态。并且弹出软键盘，但是在每次调取ajax后添加onfocus事件后，软键盘无法弹出，输入框没有焦点。

<img  src='image/signIn4.png'>

后来经过高人指点，推测有可能在ajax访问的过程中对dom有了重排，可能在onfocus已执行完毕后，页面才被重排。所以输入框没有焦点（只是推测而已）。于是乎将ajax改为同步执行，问题消失。

####获取验证码函数

手机端的登录页面总会有六十秒倒计时函数，下面贴出相应代码：


 >       var sh; 
       
        function time(o) {  //时间控制

            if (wait == 0) {

                $(".bind-getcodebtn").attr('disabled', false);

                $(".bind-getcodebtn").val("获取验证码");

                wait = 60;

            } else {

                $(".bind-getcodebtn").attr('disabled', true);

                $(".bind-getcodebtn").val(" " + wait + " 秒");

                wait--;

                sh = setTimeout(function () {

                            time(this)

                        },

                        1000)

            }

        }

希望大家能够借鉴（即使我还是个渣渣）。下面是我遇到的问题还没有解决，希望能够得到高人的解答，给input设置type为tel类型，并且一键清除按钮点击之后需要清除文本框内容并获取到焦点，在再次获取焦点时键盘会先弹出全键盘（默认键盘）后，在弹出电话号码键盘，键盘会产生闪烁现象，此现象只出现在ios客户端，推测是ios客户端响应时间比较快所以先弹出全键盘，之后判断是tel类型才出现电话键盘。但查阅各种资料后并没有查到解决方法，希望有高人能够给予解答，谢谢。 