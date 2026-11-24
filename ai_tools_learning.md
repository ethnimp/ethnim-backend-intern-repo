# Learning with Cursor

## Which tool I used

I used Cursor’s built-in Agent with Grok 4.7. The exercise used a small JavaScript function that recommends a break length based on how long a focus session lasted and whether it was completed.

## What I used it for

### Writing documentation

I asked Cursor to write a short README entry for this practice function.

```js
function getBreakMinutes(focusMinutes, completed) {
    if (!completed || focusMinutes < 25) return 0;
    return focusMinutes >= 50 ? 10 : 5;
}
```

The final README text explains that `focusMinutes` is a number and `completed` is a boolean. The function returns `0` for an unfinished session or one under 25 minutes. A completed session of at least 25 minutes and under 50 returns `5`. A completed session of 50 minutes or more returns `10`. The caller is responsible for passing the expected types.

```js
getBreakMinutes(25, true)  // 5
getBreakMinutes(50, true)  // 10
getBreakMinutes(50, false) // 0
```

### Explaining logic

I asked Cursor to explain the condition one step at a time. With a boolean input, `!completed` is true when the session is unfinished. The `||` means either condition can trigger the early return of `0`. If the function reaches the last line, `? :` chooses `10` when `focusMinutes >= 50` and `5` otherwise.

The results matched local Node.js checks. Completed sessions of 24, 25, 49 and 50 minutes returned `0`, `5`, `5` and `10`. An unfinished 60-minute session returned `0`.

## What it helped with

Cursor turned the function into a short reference with inputs, outputs and examples. Its step-by-step explanation showed why the order of the checks matters. Even a 60-minute session returns `0` if it was unfinished, because the function exits before checking the 50-minute cutoff.

## What it struggled with

Cursor’s first answer was a code comment and only showed examples for the `5`- and `10`-minute breaks. I had to ask again for README text and examples at the cutoffs. Its logic explanation also described the middle range as 25 through 49, but Node.js showed that `49.5` returns `5` too. A separate check with `getBreakMinutes(60, "false")` returned `10` because JavaScript treats non-empty strings as truthy. That showed why the documentation needed to specify a boolean input.
