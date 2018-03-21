# How to Test if a Given Value is a React.js Component


It may seem trivial, but it's a bit tricky to test for that. The [documentation for React's Test Utils](https://facebook.github.io/react/docs/test-utils.html) is lacking examples (as of the time of writing).

By comparing it with [Virtual DOM glossary](https://facebook.github.io/react/docs/glossary.html#react-components) one can assume that instantiating it with new keyword and then checking with `TestUtils.isCompositeComponent` is a way to go.

That's how I do it:

```CoffeeScript
it "is a react component", ->
  # ReactComponents can be instantiated with new keyword for test purposes
  # See https://facebook.github.io/react/docs/glossary.html#react-components
  expect (TestUtils.isCompositeComponent new CheckboxSelect)
    .to.be.ok
```

> TODO: Add a link to repo on GitHub
