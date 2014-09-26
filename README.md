CodeAnalysisJS
==============

I've only done limited testing on this, so there may be errors.

###Usage

```whitelist``` and ```blacklist``` are arrays inside ```_init()``` that can be set to whatever program flow is required.

Each array contains a list of objects that correspond to either required program statements, or disallowed program statements.

For example - 
```js
  var blacklist = [{
            type:"ForInStatement",
            message:"Please do not include a for in statement!"
        }];
```

Now whenever a user includes a ```for(var x in y)``` type statement, the message written in the blacklist will be displayed.

```js
  var whitelist: [{
        type:"ForStatement",
        message:"Please structure your program using a For statement."
  }]
```

Now whenever a user does not include a ```for (var i = 0; i < x; i++)``` type statement, the message written in the whitelist will be displayed.

###Advanced usage.

Each object in a whitelist and blacklist can have its own whitelist and blacklist.

```js
  blacklist: [{
                message: "don't include an if statement around a return statement",
                type:"IfStatement", 
                whitelist:[{type:"ReturnStatement"}]
            }];
```

In order for this blacklist object to trigger, it must also meet its own requirements.  So this object requires that if the user does include an if statement, they can't have a return statement inside of it.

Note that I did not include a message for the embedded whitelist object.  All messages are optional, but you should have at least one somewhere to make sure users aren't stuck with no feedback when they get an error.

Some more examples: 
```js
  blacklist: [{
                message: "don't include an if statement without a return statement",
                type:"IfStatement", 
                blacklist:[{type:"ReturnStatement"}]
            }];
```

This means that the user can not include an if statement unless it has a return statement inside it.

```js
  whitelist: [{
        type:"ForStatement", 
        message:"You must include a for statement",
        blacklist:[{
            type:"IfStatement", message:"You must not put an if statement in your for statement"
        }]
    }, {
        type:"ReturnStatement", message:"You must return something!"
    }],
```

The user must include a for statement, and that for statement must not have an if statement inside of it.
Additionally, the user must return at some point in their program.

Notice that even when I have one element in a whitelist or blacklist, I still wrap it in an array.  This is a requirement.

###More advanced usage than I have tested or done

You'll notice that the type parameter is pretty much the only thing being defined in each object. This is not a requirement.  You can actually check for any parameter that would be returned through the Acorn.js parser, for example, testing the parameters passed into a function, or something like that. That being said, I haven't tested that at all, so while I see no reason why it shouldn't work, I can't list it as actually supported at the moment.

