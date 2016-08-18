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

### USING [`CURL`](https://curl.haxx.se/)
```bash
(curl -sL https://goo.gl/kS3VRE > /usr/local/sbin/gmm && sudo chmod 700 gmm)
```

### USING [`BPKG`](https://github.com/bpkg/bpkg)

```bash
bpkg install -g 0x00A/gmm
```

### USING [`GIT`](https://git-scm.com/)

```bash
git clone git@github.com:0x00A/gmm.git /usr/local/lib/gmm
sudo chmod 700 /usr/local/lib/gmm/gmm
ln -s /usr/local/lib/gmm/gmm /usr/local/bin/gmm
```

# COMMANDS
There are only a handful, because really that's all you
should need. Here is some example output.

```
  git module manager v1.1.0

  usage: gmm <command> [options]

  commands:
    i, install [-v] <user/repo> [branch]   install modules
    u, uninstall <user/repo>               uninstall modules
    ls [cache]                             list installed or cached packages
    cache <update|clean>                   do stuff with the cache
    search "term" [language]               search for stuff

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
only. (This directory can be configured to be called whatever
you want using the `MODULES_LOCAL` variable).

## LIST INSTALLED MODULES

```
$ gmm ls
[INFO] listing (/Users/username/myproject)

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

## SEARCH FOR MODULES
Any search takes only a few milliseconds.

```
$ gmm search hyperterm
[OK] searching api.github.com for 'hyperterm'

📦  zeit/hyperterm - HTML/JS/CSS Terminal
    7858 ★ https://github.com/zeit/hyperterm

📦  sindresorhus/hyperterm-snazzy - Snazzy HyperTerm theme
    164 ★ https://github.com/sindresorhus/hyperterm-snazzy

📦  matheuss/hpm - ✨ A plugin manager for HyperTerm ✨
    108 ★ https://github.com/matheuss/hpm

📦  zeit/hyperpower - HyperTerm particle effects extension
    92 ★ https://github.com/zeit/hyperpower

📦  sibartlett/hyperterm-1password - 1Password extension for HyperTerm
    80 ★ https://github.com/sibartlett/hyperterm-1password

📦  staltz/hyperpunk - A cyberpunk theme for HyperTerm
    64 ★ https://github.com/staltz/hyperpunk

📦  mxstbr/hyperterm-spacegray - Spacegray theme for hyperterm
    62 ★ https://github.com/mxstbr/hyperterm-spacegray

📦  CWSpear/hyperterm-visor - Open your HyperTerm terminal from anywhere with a global hotkey.
    60 ★ https://github.com/CWSpear/hyperterm-visor
...
```


# SETTINGS
Environment variables that can be set in your shell

### `MODULES_HOME`
By default is `~/.modules`.

### `MODULES_LOCAL`
Will determine what the local modules directory should be named.
For example, you might want this to be called `node_modules` or
`cxx_modules` instead of the default which is just `modules`.

### `PROTOCOL`
By default is `git`, but can be `https`, etc.

### `HOST`
By default is `github.com`, set to whatever your git server is.

