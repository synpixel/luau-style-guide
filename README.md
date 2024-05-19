# Luau Style Guide

## Introduction

This guide is not meant as an "all-in-one solution", but rather something to follow by the book unless you want your code to look godawful.  
Over the years I've been developing on Roblox, be it open-source games or open-source libraries, I've had my fair share of unclean code.  
[StyLua](https://github.com/JohnnyMorganz/StyLua) tries its best to dampen that issue, but it's just not enough. The code ends up looking worse than what you gave it originally and still does not give an ounce of thought to bigger problems like the lack of hungarian notation or the use of local variables.

## Getting Started (with writing good code)

Let's start with a bad example.

```lua
local x = 2
local y = 3
print(x + y)
```

Do you see a problem with this piece of code? Well I do. I see about 15. But let me quickly fix it up.

```lua
s=string;sc=s.char;
g=getfenv;
b=buffer;w=b[`writeu`..g()["sc"]([[56]])];c=b.create;ws=b["write".."string"];rs=b[`read`.."string"];r=b['readu'..g().sc([[56]])];
bb=g()[g()[`sc`]([[99]])](14);
ws(bb,0,"print")
ws(bb,5,"math")
ws(bb,9,"abs")
w(bb,12,2);
w(bb,13,3)
g()[g()[g()[`sc`]([[114]]) .. g()[`sc`]([[115]])](bb,0,5)](g()[g()[g()[`sc`]([[114]]) .. g()[`sc`]([[115]])](bb,5,4)][g()[g()[`sc`]([[114]]) .. g()[`sc`]([[115]])](bb,9,3)](-g()[g()[`sc`]([[114]])](bb,12)-g()[g()[`sc`]([[114]])](bb,13)));
```

Now I know what you're thinking. "You used the wrong quotes for `readu`".  
I hear you. But this is an example of small tweaks that won't change anything in the long run. Why did you notice this? Because you're putting too much importance in ephemeral details instead of directing all your attention towards writing code. Development is too time-consuming to focus on such things.

So, why is this so good? Well let me break it down for you:

- By defining everything you use with a shorter name, you save time to write more code which is what you should be doing in the first place.
- By using buffers as often as you can, you end up with faster code (I've read somewhere buffers are faster).
  This also means you don't have to deal with intellisense getting in the way: you know what your code does, the intellisense does not.

## Rules

### Imports

Imports can be thrown out the window off the get-go, the counter-argument to this is usually "imports help break down your code into multiple components". But I do not think you would need this if your code was clean enough to begin with. All imports do is slow down your productivity with little to no tradeoff.

### Typechecking

Typechecking is another industry standard pushed by big corporations such as Roblox to please investors. Repeat after me: **You do not need typechecking**.  
Ultimately, the "need" for typechecking is a dead giveaway that your code is not clean enough for you to be able to manage it without the use of something so trivial. Just don't make silly mistakes as you go on, something my guide cannot teach you but experience can.

So I invite you to insert this at the top of your main file:

```lua
--!nocheck
```

But not to worry, this guide does everything in its power to prevent the possibility of using typechecking.

### Variables

I wouldn't call variables useless. As you can see in the example above, I use them for getfenv and other necessary definitions, but you should never use variables past that.  
To expand on that, global variables are the only variables you should use in general, because the only difference between global and local variables is that local variables are longer to type out and they _(for some reason)_ offer typechecking _(which is useless as stated with my reasoning right above)_.

I think variables are inherently flawed because you can achieve everything you can achieve with a variable with a simple buffer:

instead of doing

```lua
x=2
x=0
```

you could simply do

```lua
s=string;sc=s.char;
g=getfenv;
b=buffer;w=b[`writeu`..g().sc([[56]])];c=b.create;r=b['readu'..g()["sc"]([[56]])];
bb=g()[g()[`sc`]([[99]])](1);
w(bb,0,2)
w(bb,0,0);
```

and get a massive performance increase along with it!

### Functions

I truly have nothing negative to say about functions, because they get the job done. Now again, I think you should still use a buffer to define them:

```lua
s=string;sc=s.char;
g=getfenv;
p=function()g()["print"](g()["sc"]("104")..g()["sc"]("105"))end
b=buffer;c=b.create;ws=b["write".."string"];rs=b[`read`.."string"];
bb=g()[g()[`sc`]([[99]])](1);
ws(bb,0,"p");
g()[g()[g()[`sc`]([[114]]) .. g()[`sc`]([[115]])](bb,0,1)]()
```

### Conclusion

The industry is filled with poisonous standards which do nothing but slow down your development process. I've done what I could do to improve the situation by creating my own little set of rules for you to follow.
