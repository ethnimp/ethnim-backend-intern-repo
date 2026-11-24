# AI Tools for Development

## Which AI tools did you try?

I used ChatGPT through the Codex desktop session, which was already set up on my Mac. For the exercise, Codex generated a small JavaScript function that counts completed focus sessions and adds up their minutes. We used sample data and ran the code locally in Node.js.

## What worked well? What didn’t?

The generated function was easy to follow. The sample had two completed sessions of 25 and 5 minutes, plus an unfinished session of 15 minutes. The function correctly returned two completed sessions and 30 minutes. The checks for an empty list and a list with no completed sessions also passed.

The first version of the caller broke when it tried to summarise sessions loaded by an `async` function. It passed a Promise to code that expected an array, and Node.js returned `TypeError: sessions is not iterable`. Codex reproduced the error and changed the caller to wait for the array before passing it to the summary function.

```js
async function loadAndSummariseSessions(loadSessions) {
    const sessions = await loadSessions();
    return summariseSessions(sessions);
}
```

The explanation helped me understand that an `async` function returns a Promise. Using `await` inside the caller gives it the resolved value before the next line runs. The revised code returned the expected summary, and a separate check confirmed that a failed load still surfaced an error.

## When do you think AI is most useful for coding?

I think AI is most useful when I can give it a small example, explain what I expect, and check its answer. It helped turn a confusing error into something concrete I could follow in the code. As I learn Node.js, I’d use it to explain concepts with examples and suggest what to test, then run those checks before relying on the code.
