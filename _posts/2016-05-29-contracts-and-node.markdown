---
layout          : post
title           : "contracts and node.js pt. 1"
date            : 2016-05-29 23:33:16 
categories      : bettercoding 
---

design by contract
-------------------------------------------------------------------------------

The concepts of design by contract should be very familiar to most developers 
coming up today. When you write a piece of code, write it so that it can be 
tested. Give your code a set of clear tolerances that it is guaranteed to 
operate within, then design safeguards to prevent it from operating if those
conditions are not met. 

At first glance, you might think that this is just a primitive form of test
driven development. You wouldn't be wrong, but you wouldn't be right. Done 
properly, design by contract provides a much richer set of constraints that
liberate the developer and promote better code. The key difference is that you
don't start with the tests, you start with the specification. I am not going 
to go into a long discourse about design by contract here, there are plenty 
of sources that would do a better job than me. I would start with the original
- [Bertrand Meyer and Eiffel](https://www.eiffel.com/values/design-by-contract/introduction/)

adding it in
-------------------------------------------------------------------------------

Node.js has quickly become my go to language to get dirty work done quickly. It 
is simple, asynchronous, and a *common tounge* that a wide variety of developers
can understand. The biggest issue I have with javascript is that it is a 
scripting language that has been taken far beyond anything that it was 
originally meant to do. If you have read any of my previous posts, that's a big
deal for me.

I (obviously) got past that in this case. I feel that node is well designed and
gets the job done in a way that allows interactions that would not be possible
in a lot of other frameworks. Unfortunately, node (and just about every other
language) does not support a native way to implement design by contract in an 
intuitive fashion. 

overcoming preconceptions
-------------------------------------------------------------------------------

I **hate** the concept of .NET. I don't mind code generators as long as you 
know what they are doing. .NET is another animal. The *Common Language Runtime*
thing has always bugged me. *You can write in whatever language you want, it's
still going to be crap though.*

That notion is why I have always avoided node.js aids like CoffeeScript. Sure,
it provides you with a handy way to write javascript so it looks like ruby, but
all it does is spit out javascript, right? If you took the time to learn 
javascript, would you have done it differently? Maybe, maybe not. I'm just not
a fan of that. Want Ruby? Write Ruby. I just wanted to make that fact clear 
before I tell you to install [Babel](https://www.npmjs.com/package/babel).

the fix
-------------------------------------------------------------------------------

I evaluated several different options that looked like they may do what I 
wanted. Most I discounted because it added too much overhead to writing code or
it just *didn't work* out of the box. Finally, I settled on a solution that 
required Babel as a *compiler*.

Yes, my stomach reeled at the thought of *compiliing* javascript, but I thought
I would try it anyhow. I was pleasantly surprised.

Instead of a lot of commentary, you can try it out for yourself. I set up my 
package directories like so:

~~~~
package/
  lib/
  setup/
  spec/
  src/
  package.json
~~~~

In this structure, my *compiled* files are housed in lib, config hook scripts
end up in setup, spec has the tests, and src is the raw code. So, assuming that
you use this structure (modify if you do not), you can get started with the 
following.

~~~~
npm install babel -save-dev
npm install babel-plugin-contracts -save-dev
npm install mocha -save-dev
npm install chai -save-dev
~~~~

This will set you up with a pretty solid development and testing framework. 
Now you need to set up a *.babelrc* file in your plugin directory. Unlike a 
lot of the documentation, I always leave my assertions **ON**. Why? Well, 
unless you do a lot of crazy stuff in your assertion, it doesn't really kill
performance does it? All it can do is help.

~~~~
{
  "plugins": [
    [
      "contracts", {
        "env": {
          "production": {
            "strip": false
          }
        }
      }
    ]
  ]
}
~~~~

contract away
-------------------------------------------------------------------------------

Once this is set up, you can weave contracts into your normal code. It is 
always a good practice to do this up front (before you write the methods AND
in the beginning of your methods). Specify your preconditions and 
postconditions, make some assertions, get crazy.

~~~~
function splitLine(line) {
  var originalLine = line;
  pre : {
    typeof line === 'string', 'must provide a string value';
    line.length > 80, 'line must be longer than 80 characters';
  };
  post: {
    originalLine === line, 'must not change input value';
  }

  [A BUNCH OF STUFF HAPPENS]
}
~~~~

[Codemix](http://codemix.com/) did a very good job of providing a simple syntax
that does what you need it to, and nothing that you don't. The generated code
is clean and understandable by just about everyone. 

play with it
-------------------------------------------------------------------------------

Before you delve too much deeper, get in and play with it. Never hurts. I'll 
get into testing a little tomorrow.
