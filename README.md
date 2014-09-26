CodeAnalysisJS
==============

###Usage

```whitelist``` and ```blacklist``` are arrays inside ```_init()``` that can be set to whatever program flow is required.

Each array contains a list of objects that correspond to either required program statements, or disallowed program statements.

For example - 
```js
  var blacklist = [{
            type:"ForInStatement",
            message:"Do not include a for in statement!"
        }];
```

Now whenever a user includes a '''for(var x in y)''' type statement, the message written in the blacklist will be displayed.

```js

```

###Advanced usage.
