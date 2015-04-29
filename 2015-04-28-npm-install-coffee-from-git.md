How to install npm packages written in coffee-script from git repo
==================================================================

> TODO: Why

  * Example repo

> TODO: How

IDEA: Use npm `install` script with value same as `prepublish`, but this would have to be changed before publishing to registry.

It is said to be an antipattern

See https://docs.npmjs.com/misc/scripts#common-uses

An issue by isaacs [run `prepublish` for git url packages][npm-npm-3055]

Installing it from a directory (`../package/`) runs `prepublish`. WTF?

> IDEA: Make a gitinstall gulp task, which will:

* npm install (to get dev dependencies)
* run build task

Would it be possible use .npmignore then?

The problem is that gulp is in dev-dependencies. So npm install has to be in install script, which seems a little strange.

Result: endless loop (npm install triggers install script; obviously).

> NOTE: Installing from local directory triggers prepublish

Maybe installing from git should work like that:

1. clone to tmp dir
2. install from tmp dir
3. remove tmp dir

This doesn't seem very hard to do.

> TODO: Ask in #3055 is this good approach

[npm-npm-3055]: https://github.com/npm/npm/issues/3055
