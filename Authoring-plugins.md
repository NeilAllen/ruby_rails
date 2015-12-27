rbenv plugins provide new commands and/or hook into existing functionality of
rbenv. The following file naming scheme should be followed in a plugin project:

1. `bin/rbenv-COMMAND` for commands
2. `etc/rbenv.d/HOOK_NAME/*.bash` for hooks


## rbenv commands

An rbenv command is an executable named like `rbenv-COMMAND`. It will get
executed when a user runs `rbenv COMMAND`. Its help will be displayed when a
user runs `rbenv help COMMAND`. It can be written in any interpreted language,
but bash script is recommended for portability.

**A plugin command can't override any of the rbenv's built-in commands.**

### Environment

Each rbenv command runs with the following environment:

* `$RBENV_ROOT` - where rbenv versions & user data is placed, typically `~/.rbenv`
* `$RBENV_DIR` - the current directory of the caller
* `$PATH` - constructed to contain:
  1. rbenv's `libexec` dir with core commands
  1. `$RBENV_ROOT/plugins/*/bin` for plugin commands
  1. `$PATH` (external value)

### Calling other commands

When calling other commands from a command, use the `rbenv-COMMAND` form (with
dash) instead of `rbenv COMMAND` (with space).

Use rbenv's core low-level commands to inspect the environment instead of doing
it manually. For example, read the result of `rbenv-prefix` instead of
constructing it like `$RBENV_ROOT/versions/$version`.

A plugin command shouldn't have too much knowledge of rbenv's internals.

### Help text

An rbenv command should provide help text in the topmost comment of its source
code. The help format is described in `rbenv help help`.

Here is a template for an executable called `rbenv-COMMAND`:

```sh
#!/usr/bin/env bash
#
# Summary: One line, short description of a command
#
# Usage: rbenv COMMAND [--optional-flag] <required-argument>
#
# More thorough help text wrapped at 70 characters that spans
# multiple lines until the end of the comment block.

set -e
[ -n "$RBENV_DEBUG" ] && set -x

# Optional: Abort with usage line when called with invalid arguments
# (replace COMMAND with the name of this command)
if [ -z "$1" ]; then
  rbenv-help --usage COMMAND >&2
  exit 1
fi
```

### Completions

A command can optionally provide tab-completions in the shell by outputting
completion values when invoked with the `--complete` flag.

``` sh
# Provide rbenv completions
if [ "$1" = "--complete" ]; then
  echo hello
  exit
fi
```

Note: **it's important to keep the above comment intact**. This is how rbenv
detects if a command is capable of providing completion values.


## rbenv hooks

Hooks are bash scripts named like `HOOK_NAME/*.bash`, where "HOOK_NAME" is one
of:

* `exec`
* `rehash`
* `version-name`
* `version-origin`
* `which`

Hooks are looked for in `$RBENV_HOOK_PATH`, which is composed of:

1. `$RBENV_HOOK_PATH` (external value)
1. `$RBENV_ROOT/rbenv.d`
1. `/usr/local/etc/rbenv.d`
1. `/etc/rbenv.d`
1. `/usr/lib/rbenv/hooks`
1. `$RBENV_ROOT/plugins/*/etc/rbenv.d`

Hook scripts are executed at specific points during rbenv operation. They
provide a low-level entry point for integration with rbenv's functionality. To
get a better understanding of the possibilities with hooks, read the source
code of rbenv's hook-enabled commands listed above.
