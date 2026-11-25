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

## Naming Variables and Functions

### What makes a good name?

A variable name should tell me what the value represents. For durations, I include the unit when it matters, as in `elapsed_seconds`. A function name should describe its action or the question it answers. `has_reached_focus_goal` makes it clear that the result is true or false. In Python I use lowercase words separated by underscores and follow the project’s naming conventions.

### What issues can unclear names cause?

Names like `a` and `b` hide the difference between a target in minutes and elapsed time in seconds. A caller could swap the arguments or pass minutes for both. The arithmetic would still run and could report the wrong result without raising an error.

### Before renaming

```python
def check(a, b):
    c = a * 60
    return b >= c
```

### After renaming

```python
def has_reached_focus_goal(goal_minutes, elapsed_seconds):
    goal_seconds = goal_minutes * 60
    return elapsed_seconds >= goal_seconds
```

### How did refactoring improve readability?

The new names make the conversion easy to follow. The function converts the goal to seconds and checks whether the elapsed time has reached it. A call like `has_reached_focus_goal(goal_minutes=25, elapsed_seconds=1500)` makes the inputs clear at the call site too. I checked both versions just below, exactly at, and above the 25-minute goal. Both returned `False`, `True`, and `True` respectively.
