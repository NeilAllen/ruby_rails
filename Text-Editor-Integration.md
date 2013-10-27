## TextMate
1. Preferences → Variables
1. add this to the front of `PATH`: `$HOME/.rbenv/bin:$HOME/.rbenv/shims:`
2. set `TM_RUBY` to this: `$HOME/.rbenv/shims/ruby`
4. (and make sure the checkboxes for each of those variables is selected)

These instructions will use rbenv’s global version of ruby. If you want to fix it to some other specific version, populate `RBENV_VERSION`. example: `2.1.0-preview1`. For some commands it will probably be desirable to use your project’s version of ruby. To do so you would need to intelligently read the version from the project root’s .ruby-version file and set it dynamically. I (@jjb) don’t have the TextMate-Fu to achieve this — if you know of a way, please share!

