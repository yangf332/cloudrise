
Vim 常用操作
============================

## 移动
    hjkl - 左下上右
    GG - 第一行; 
    [Shift] + G - 最后一行
    [Shift] + H(Head);    // 当前屏幕最上方
    [Shift] + M(Middle);  // 当前屏幕中间
    [Shift] + L(Last);    // 当前屏幕最下方
    |
    0 // 移动到行首
    [Shift] + $ // 移动到行尾
    [Shift] + ^ // 移动到行第一个字符
    |
    [Ctrl] + f // 下翻一页
    [Ctrl] + b // 上翻一页
    [Ctrl] + d // 下翻半页
    [Ctrl] + u // 下翻半页
    |
    [Shift] + *  // 查找光标所在处单词，向下查
    [Shift] + #  // 查找光标所在处单词，向上查
    [Shift] + %  // 跳到与之匹配的括号处


## 编辑
    yy    // 复制一行
    yw    // 复制一个单词
    y[n]w // 复制n个单词
    |
    dd    // 剪切一行
    dw    // 剪切一个单词
    d[n]w // 剪切n个单词
    |
    p  // 粘贴内容
    :reg  // 显示保存的剪切内容
    "[n]p // 粘贴标记n的剪切内容
    |
    i  // 当前处插入
    a  // 后面插入
    |
    :n1,n2s/word1/word2/gc // 从n1行到n2行，把word1替换为word2,g为全局,c为需确认
    |
    gU     // 选中内容变大写
    gu     // 选中内容变小写
    |
    [ctrl] + v , [shift] + 操作[i|a] // 块操作
    |
    >>
    <<

## 书签
    m[a]     // 设置书签a
    '[a]     // 移到书签a

## 其它

    =     // 整理格式 
    |
    :set nu   // 显示行号
    :set nonu // 取消行号
    |
    :set ts=4 
    |
    :sp [filename]  // 分割屏幕打开filename文件
    :vsp [filename] //
    行首加入内容  :%s/^/addtext
    行尾加入内容  :%s/$/addtext

## .vimrc
    cd ~
    vim .vimrc
    syntax on
    set nu
    set ts=4
    set ruler
    set expandtab
    set tabstop=4
    set softtabstop=4
    set shiftwidth=4
    set autoindent
    set encoding=utf-8
    set termencoding=utf-8
    set cursorline

## .bashrc
    cd ~
    vim .bashrc
    alias ll='ls -l --color=tty'
    alias ls='ls --color=tty'
    alias grep='grep --color=tty'
     

##以下内容来自网络其它地方
    [简明 Vim 练级攻略](http://coolshell.cn/articles/5426.html?jtss=tsina)
