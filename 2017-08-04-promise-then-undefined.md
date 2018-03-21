# Passing `undefined` to a JavaScript promise

Consider this simple snippet:

```JavaScript
Promise
  .resolve('JavaScript, why are you doing this to me?')
  .then(console.logg)
  .catch(console.error)
```

Note that `console.logg` is `undefined`. What will be printed?

**Nothing**.

The promise will silently resolve to the value of

```JavaScript
'JavaScript, why are you doing this to me?'
```

Which is a good question. I think it's because it hates me.

It's obviously a developer's mistake. My first thought was that introducing type system (like Flow) would solve this - and it would. But why isn't `then` method of a `Promise` just throwing a type error as soon as anything other than `function` is passed to it?

This obviously leads to silent and hard to spot bugs. Unfortunately in JS community there is a strong attitude of ignoring the errors and going on as if nothing ever happened.
