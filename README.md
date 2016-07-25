# SYNOPSIS
git module manager

# MOTIVATION
Simpler, faster, less complex dependency management!

Submodules receive much praise and criticism. Yet both depend
on the interpretation of how they should be used; `gmm` focuses
entirely on providing a workflow for dependency management.

Don't edit submodules — it's not an easy git workflow to manage.
This is also the basis of most submodule criticism. Instead, use
them as immutable dependencies, when you need changes, publish
them from upstream and simply re-install using `gmm`.

# STATUS
Idea/Work in Progress

# INSTALL GMM
You can just run this simple one-liner to install. The google-
shortened link points to the raw github user content (paste it
in the url-bar of your browser to verify). The sudo prompt for
your password is the chmod command asking for your permission
to make the file executable.

```bash
(curl -sL https://goo.gl/kS3VRE > /usr/local/sbin/gmm && sudo chmod 700 gmm)
```

You can also use [bpkg](https://github.com/bpkg/bpkg) to install `gmm`.

```bash
bpkg install -g 0x00A/gmm
```

# COMMANDS
There are only a handful, because really that's all you
should need. Here is some example output.

```
  git module manager v1.0.0

  usage: gmm <command> [options]

  commands:
    i, install [-v] <user/repo> [branch]   install modules
    u, uninstall <user/repo>               uninstall modules
    ls [cache]                             list installed or cached packages
    cache <update|clean>                   do stuff with the cache

  options:
    --help, -h              show this help information
    --version               print the version number
    --update                self update
```

## INSTALL MODULES
Install first clones the repo to your `~/.modules` cache, then
adds it to your project from the cache.This is nice for
performance and offline usage.

Install will ensure your working tree is clean before adding a
submodule. Then, it will add the submodule (at the specified
branch, or master by default), then commit it for you.

```
$ gmm i someorg/somerepo
[OK] pulled latest from git://github.com/someorg/somerepo.git
[INFO] using cached version
[OK] added the submodule
[OK] submodule installed
```

Once your submodule is installed you will see a `modules`
directory in your project, these files will be flagged as read
only.

## LIST INSTALLED MODULES

```
$ gmm ls
[INFO] listing (/Users/username/workroot/0x00a/gmm)

[INFO] 📦  foo@master in ./modules/someorg/foo
[INFO] 📦  quxx@0.1.0 in ./modules/someorg/quxx

[OK] found 2 module(s) in myproject
```

## LIST CACHED MODULES
The cache will **try** to update every time you install. But if
you want to update all items in your cache, you can run the
`gmm cache update` command.

```
$ gmm ls cache
[INFO] listing cache (/Users/username/.modules)

[INFO] 📦  foo in /someorg/foo
[INFO] 📦  quxx in /someorgb/quxx

[OK] found 2 repos
```

