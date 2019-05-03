title: C++ Pointer WTF
author: wuyuema
tags:
  - 琐碎
categories: []
date: 2019-05-01 02:54:00
---
今天总算知道为什么都不建议OIer用指针了......  
真的是太~~TMD~~容易出错了。  
<!--more-->
举个例子：
```cpp
_node *newnode(_node *u, _node *v, T cont = 0) {
	_node *tmp = new _node();
    tmp->last = u, tmp->next = v, tmp->data = cont;
    return tmp;
}
...
int main() {  
    ...
    _node *HEAD, *TAIL;
    HEAD = newnode(NULL, TAIL);
    TAIL = newnode(HEAD, NULL);
    ...
}
```
__想象__：我这样写，HEAD和TAIL不就互相link了么？只用了两行简洁的代码（自我陶醉）  
__事实__：恭喜你，在`TAIL = newnode(HEAD, NULL)`执行之后，你的TAIL就不再是以前的那个TAIL了。   
就是这样，你GG了。  
分析代码，不难发现newnode()函数在每次使用时都会改变指针的值。  
因此，指针看起来很安全方便，实际上很容易让人给自己挖坑。  

```cpp
补充：要想像上面一样直接用指针赋值，请使用双指针。
_node **HEAD, **TAIL;
*HEAD = newnode(NULL, *TAIL);
*TAIL = newnode(*HEAD, NULL);
//unexperimented
```