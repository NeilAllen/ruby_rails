The beauty of rbenv is that **it doesn't require special integrations** with any
tools, shells or environments. Its shims directory just needs to be present in
the path and rbenv will take care of the rest.

The following is practial info on how to add `~/.rbenv/shims` to `PATH` in
various programs/environments.

## TextMate

In _Preferences → Variables_, prepend this to `PATH`:


```sh
$HOME/.rbenv/shims:
```

## Sublime Text 2

_Tools → Build System → New Build System_:

```json
{
  "cmd": ["ruby", "$file"],
  "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
  "selector": "source.ruby",
  "path": "$HOME/.rbenv/shims:$PATH"
}
```

Save this new build system as "Ruby rbenv" or similar so you can distinguish it
from the built-in "Ruby" build system.

## Capistrano

Add to your Capistrano recipe:

```rb
set :default_environment, {
  'PATH' => "$HOME/.rbenv/shims:$PATH",
}
```

## Post-receive git hook

The post-receive script that runs on a remote machine as a result of git push
will run in a restricted shell and therefore won't source any init files
described in [[Unix shell initialization]]. As a consequence, rbenv won't be
present in PATH even if you configured it to be enabled when you log in over SSH.

The solution is to explicitly define PATH as descibed in cron section below.

## cron jobs

Explicitly define PATH at the top of your crontab file:

```sh
PATH=/Users/mislav/.rbenv/shims:/usr/local/bin:/usr/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin
```
