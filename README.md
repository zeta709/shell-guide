# shell-guide

Personal shell script guide.

## Control statements

### Prefer `good_condition || return 1` to `bad_condition && return 1`

#### What you want:
You may want to replace a simple `if` block with a one-liner.
``` sh
func_intended() {
    # ...
    if [ -z "$SOME_VAR" ]; then
        printf "ERROR\n"
        return 1
    fi
    return # info: $? is 0
}
```

#### Problematic code:
``` sh
func_problematic() {
    # ...
    [ -z "$SOME_VAR" ] && { printf "ERROR\n"; return 1; }
    return # warning: $? is 1
}
```

#### Correct code:
``` sh
func_correct() {
    # ...
    [ -n "$SOME_VAR" ] || { printf "ERROR\n"; return 1; }
    return # info: $? is 0
}
```

#### Note:

It seems the current version of ShellCheck fails to find this kind of programming errors at the time of writing.
It detects an issue in code like `A && B || C` but it is a different type of problem.
See ShellScheck [SC2015](https://github.com/koalaman/shellcheck/wiki/SC2015) regarding `A && B || C`.

## Code snippets

See [wiki](https://github.com/zeta709/shell-guide/wiki) for code snippets.

## References

[ShellCheck](https://github.com/koalaman/shellcheck) is a great tool.
