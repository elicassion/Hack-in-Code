# Hack-in-Code
About mines, clever tricks and wicked craft in coding

# JavaScript

## The different mechanisms of `this` in `()=>` and `function(){}`
In ECMA6, `()=>` is a new method to define an anonymous function. 
However, it is not totally equal to `function(){}`. 
Several pieces of my code trying to use `()=>` to replace `function(){}` involving `this` failed to implement the target function.
The key is the difference between their ways handling `this`.

`()=>` deals with `this` by inheritance, where it has no `this` for itself. 
`this` in arrow function is inherited from its outer function.
For example:

```javascript
function foo(){
    return () => {
        return () => {
            return () => {
                console.log(this.sth);
            }
        }
    }
}
foo.call({sth:bar})
```
There is only one time of binding `this` happenning when executing this piece of code.
When `this` is not declared in arrow functions, it will seek recursively outside each function to find a place where `this` exactly exists.
The mechanism is just like the approach to use local variables.

As for `function(){}`, `this` is just the object calls the function.
Generally, if using `obj.func`, `this` is `obj`. 
If no one is found calling `function()`, `this` will be `window` under the default environment or be `undefined` in "strict mode".
