---
layout          : post
title           : bad things, meet good code
date            : 2016-05-20 23:33:16 -0600
categories      : bettercoding 
---

hide your keys
-------------------------------------------------------------------------------

We've all written terrible code. The kind of code that steals your car in
the middle of the night and robs a liquor store. We don't mean to. Most of
the time it happens because we don't know any better. Sometimes it happens 
when we just don't care. The rest of the time, we usually have the best 
intentions. It started out as pretty solid code. We stuck to our guns, made
contracts, wrote some tests. You can't really put a finger on when it went 
bad, it just did.

### it is always your fault (sorry will)

There will be situations where naughty code seems inevitable. You will face 
them. In fact, I don't recall a situation that I was in when there wasn't a 
good excuse to have filthy, buggy code. That's all they are though... excuses.

### merry christmas, hope you like crap

By far, the most convenient excuse is that you didn't write the initial 
code. It was given to you, inherited. Some tool who is long gone and can't 
defend his(or her)self anymore did... and it's all their fault. The best you 
can do is just write patches in the same style and hope for the best. Testing? 
Documentation? He or she didn't feel the need, why should you?

### cats in the cradle

There is always a time crunch. Always a compromise to be made. Quality control 
is superfluous, right? You work for a startup, you just need to ship code. It 
just a website (or app) patches are cheap. Time is the real currency.

stop it
-------------------------------------------------------------------------------

So... what's the silver bullet? Sadly, there isn't one. The best you can do is
stick to your guns. See the trap before you fall into it. Go around it, or 
make a bridge to get over it. Don't just cover it up and pretend it's not 
there.

Go into every new job or project you take over with the knowledge that there
have been compromises made. Also know that the tool who wrote it is someone 
just like you (most of the time). Pressure turns coal to diamonds. It can do 
the same to code from time to time, but most of the time it just turns to poo.

### be deliberate

Take the time to review the existing code. You need to know it down to its last
hairy wart. Flag the naughty parts. When you write new code, make sure that it
does what you mean it to and fails when the rest of the application gives it 
junk. If there are no unit tests in a project, make sure you write them for 
your changes. When you have a moment, go back and refactor. For every piece of 
new work, write contracts, leave on assertions, test the crap out of it.

### it's only your good name

Remember that when you are done, *you will be that tool*. There will be 
someone who maintains your code after you do (without exception). Would you 
rather the next guy curse you as the guy who wrote trash code or have him
curse you for being the anal retentive ass who wrote all the tests and that
your code is so strict that it doesn't allow junk in? I'll take the later.

appendix: fallacies (all of these are false)
-------------------------------------------------------------------------------

+ you don't need to write unit tests
+ automation is only important when the project is mature
+ you can ship it without documentation
+ there isn't enough time to do (x)
+ the program has always done that, nothing I can do about it
+ this method can not fail
