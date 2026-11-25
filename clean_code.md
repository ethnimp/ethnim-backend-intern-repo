# Clean Code

## Five principles

- **Simplicity.** Use the fewest steps needed to express the rule clearly. A small calculation can often fit in one function.
- **Readability.** Use names that explain what values represent. Someone reading the code should be able to follow the calculation without tracing every assignment.
- **Maintainability.** Keep related logic together and give each function one clear job. That makes it easier to find where a rule needs to change and to check the result.
- **Consistency.** Follow the project’s conventions for naming, spacing, and layout so that files are easy to read across the codebase.
- **Efficiency.** Avoid work the program can easily skip. If performance becomes a problem, measure where the time or memory goes before adding complexity.

## Example

Both Python functions take a list of focus sessions and return the total minutes from completed sessions. If the list is empty, the total is zero.

### Messy version

```python
def f(a):
    r=[]
    for i in range(len(a)):
        if a[i]["completed"]:
            r.append(a[i]["minutes"])
    t=0
    for j in range(len(r)):
        t=t+r[j]
    return t
```

I have to read the whole function to understand what `f` returns or what `a`, `r`, and `t` represent. The first loop collects minutes in a temporary list. The second loop adds them up. The index lookups and tight spacing make the calculation harder to follow.

### Cleaned-up version

```python
def total_completed_minutes(sessions):
    total_minutes = 0

    for session in sessions:
        if session["completed"]:
            total_minutes += session["minutes"]

    return total_minutes
```

The function name describes the result, and `session` and `total_minutes` explain the values. Iterating over each session directly removes the index lookups. Adding the minutes as each completed session is found also removes the temporary list and the second loop. The completion rule and the calculation now sit together.

I ran both versions with a 25-minute completed session, a 10-minute incomplete session, and a 5-minute completed session. Both returned 30. I also checked empty lists, lists with only incomplete sessions, and lists with only completed sessions.
