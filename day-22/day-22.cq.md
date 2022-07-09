# Network requests

> We typically use `fetch` to make network requests for JSON data.

Most apps will access the internet in one way or another. Today we'll be looking at one of the most common forms of this: calling an API and handling a JSON reponse object using `fetch`.

React Native supports most of the same networking APIs as web browsers, like `XMLHttpRequest` and `fetch`. This means that libraries you might already be familiar with, like `superagent` or `axios`, should work out-of-the-box. Additionally, there are third-party libraries for supporting more advanced use cases, like Apollo for GraphQL.

## But first... `async` and `await`

If you already know how to use the JavaScript keywords `async` and `await`, skip ahead to the next section. Otherwise, here's a quick primer.

The keywords `async` and `await` are a useful JavaScript language feature for handling control flow in asynchronous programs. These leverage the `Promise` class under the hood, and are an alternative to many patterns that previously used callbacks.

To use these:

- We write `async` before a function definition. This _forces the function to return a `Promise`_. No matter what we `return` from an `async function`, the value will be wrapped in a promise if it isn't already.
- We write `await` before a `Promise` to pause the execution of the current function until the `Promise` is resolved or rejected. This pause is _non-blocking_, so other code can still run if triggered by a browser/`node` event. We can _only use `await` within an `async` function_.

Here's an example:

```js
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

// This function returns Promise.resolve(42), since it's marked as `async`
async function getNumber() {
  return 42;
}

async function main() {
  console.log("hello"); // => "hello"
  await sleep(1000); // wait 1000ms
  console.log("world"); // => "world"
  const number = await getNumber(); // unwrap the 42 from its promise
  console.log(number); // => "42"
}

main();
```

In this example, we created a `sleep` function that waits for `ms` milliseconds using `setTimeout`. We also created a `getNumber` function that doesn't actually do anything asynchronous, but still wraps its result in a `Promise` since it's marked as `async`. Lastly, we call these from a `main` function using `await`. Sometimes we may ignore the result of an `await`-ed function, like `sleep`. Other times we may use the value, as in the case of `getNumber`.

If an error is thrown in an `async` function, the function will then return `Promise.reject(error)`. If an `await`-ed `Promise` is rejected, the error value is thrown -- so most `await` calls should happen in a `try/catch` block.

We commonly use `async` and `await` for network calls, as we'll see now!

## `fetch`

We typically use `fetch` to make network requests for JSON data.

Here's an example where we fetch a list of posts from a placeholder data API:

```js
async function fetchPosts() {
  const result = await fetch("https://jsonplaceholder.typicode.com/posts");
  const posts = await result.json();
  return posts;
}
```

The call to `fetch` returns a `Promise`, so we use `await` to pause execution of the function until the `Promise` resolves. After that, we convert the response to a JavaScript object using `result.json()`, which is also asynchronous and returns a `Promise`. Finally, we return the result from our function.

Here's what a component that uses `fetchPosts` might look like:

<iframe src="https://snack.expo.io/embedded/@dabbott/network-requests?preview=true&platform=web" style="height: 37em;border:1px solid rgba(0,0,0,.08);border-radius:4px;background:center no-repeat url('https://i.imgur.com/5apDm5w.gif'), #fafafa;" />

[Download example](https://expo.io/--/api/v2/snack/download/@dabbott/network-requests)

### Up next

Fetching data from the internet is great, but one of the big advantages of mobile apps is that we can make the data available offline. To do that, we'll need to persist the data we fetch. Check out tomorrow's article to see how!
