Using `Promise.race` in Node.js to enforce a timeout
====================================================

It is a little bit more tricky than this:

```js
const task = new Promise((resolve, reject) =>
  setTimeout(resolve, 5000, 'done')
)

const timeout = new Promise((resolve, reject) =>
  setTimeout(reject, 100, 'timed out')
)

Promise
  .race([
    timeout,
    task
  ])
  .then(console.log)
  .catch(console.error);
```

If you run this, you will find out that the process terminates only after both promises are done (i.e. after around 5 seconds):

```shell
$ time node src/race.js
timed out
node src/race.js  0,36s user 0,03s system 7% cpu 5,370 total
```

In fact, if one of them is never resolved (and that's exactly what we expect, otherwise we would not introduce a timeout here), the process will hang forever. Seems like `Promise.race` is not doing a proper cleanup. The `task` promise remains pending (event though it's eventual value will never propagate through the chain). This makes the runtime wait for it's resolution before it terminates.

Unfortunately I don't know of any elegant workaround for this. Currently I simply call `process.exit` somewhere down the chain:

```JavaScript
Promise
  .race([
    timeout,
    task
  ])
  .then(console.log)
  .catch(console.error);
  .then(process.exit)
```

In my book it's not an elegant solution.
