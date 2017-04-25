<img src = "https://s-media-cache-ak0.pinimg.com/736x/06/f0/ee/06f0eeac077f1c29a3b4924ced5f34e4.jpg">









Why F# Sucks?


**!!!DISCLAIMER!!!**

I am totally in love with F#, but there several cases where I find it irrationally bad.
These cases are the reasons why I don't want to do pure FP @ .NET, there are a lot of situations where OOP C# fits much better than F#.
Every time you learn something new, you invest your time and want to make a profit of it. It looks well every time till you don't watch on the other side. Nothing is perfect and you know it, right?
So let me tell you several points about F# & FP that will make you think twice before switching to it.






**Allocations and how do they affect performance**

<img src = "https://media.makeameme.org/created/oh-functional-programming.jpg"/>

Imagine you have a progress bar. Functional paradigm tells us not to change value of progress bar indicator, but to create a new progress bar with changed indicator value, return it and assign to the old one.
Here you must ask yourself about allocations, think about every-row allocations and hope for the best, hope that compiler will inline everything for you. But eventually it won't, I'm sorry.


**Tooling**

As a C# developer, I'm used to ReSharper. I don't want to write code by myself when I can auto-generate it by pressing Alt+Enter.
How do Visual Studio or VS Code support me in this field? Very and very sketchy. Imagine a situation that you have interface in your F# code, you need to use it, but you don't remember exact signature of it. Well, you are done here. Because your IDE won't help you, there is no ReSharper magic here, Visual Studio by itself doesn't know about your interface. Most of the times you will Ctrl+F and search for interfaces, some of the times you will try to recollect name from your memory. Wasting time. VS itself is slow, now you are loosing even more time.

BUT !!!

You can use Visual Studio Code which is great IDE by Microsoft as well.
And very soon I suppose you would be able to use Rider .NET IDE by JetBrains for F# development. It's unreleased for 4/24/2017, but they already made an announcement (link twitter)

I hope that someday F# won't have that bad tooling and we'll be able to write more code with less actions.

**Marketing went totally wrong**

Try to search for Fake on Google. You won't find a proper result, instead you need to google F# make.
Try to search some big F# projects. F# is not new language, but Microsoft for some reason doesn't develop it as they should.

**Complexity of language**

Do you know that F# has like 100+ operators? And you can define your own ones manually.
That produces complexity and makes code less understandable.

<img src = "http://image.prntscr.com/image/2b4d0e8bab8a4c9c968983ed01a8e913.png"/>
<a href = "https://twitter.com/kot_2010/status/856123414637146112">src</a>

Have you ever worked on a project with junior developer that is pretty ambitious and wants to show that junior isn't his level, that he can write really cool code.
In his point of view cool code = complex code. And then you just look at his code and trying to figure out what is going on for like 10 minutes. Life is hard.
Well, that's basically me.
However, not only junior developers do that. So in F# you can write equal parts functions in a lot of different ways.

EXAMPLE two different realizations of equal parts.


**Integration with C#**

On every F# speech I hear a question about integration F# functions into C# code as libs or w/e. And every time I hear the same answer:

> Yes, you can do it, we trust in you! F# is well integrated in C#!!!

However, that's not true.
I've got 2 points here:
  * there are a lot of types that need to be casted from F# to C#. e.g. F# list is different from C# list.
  * have you ever tried to integrate big F# parts in your C# solutions? That just look weird: calling functions from static class between a bunch of object oriented code. At this point you should ask yourself like why there is functions in my C#. And the next developer that will maintain your C# code with integrated F#, he will ask himself twice and so on.


**Is FP even worth it?**

You know what - at some point C# will eventually steal everything that is worth stealing. That's what we see in C# 7.0 - tuples, pattern matching, local functions and etc. async was introduced in F# in like 2007, C# got it in 2012. There is the question of time, but anyway C# is a big-player programming language with a super big community, that's reasonable.
Check this Mark Seeman's <a href ="http://blog.ploeh.dk/2015/04/15/c-will-eventually-get-all-f-features-right/">post</a> out.
