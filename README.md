# SYNOPSIS
git module manager

# MOTIVATION
Simpler, faster, less complex dependency management!

# STATUS
Idea/Work in Progress

# COMMANDS
There are only a handful, because really that's all you
should need. Here is some example output.

```
  git module manager v1.0.0

  usage: gmm <command> [options]

  commands:
    i, install [-v] <user/repo> [branch]
    u, uninstall <user/repo>
    ls
    cache [ls|clean]        do stuff

  options:
    --help, -h              show this help information
    --version               print the version number
```

### INSTALL MODULES

```
$ gmm i voltraco/docs
[OK] pulled latest from git://github.com/voltraco/docs.git
[INFO] using cached version
[OK] added the submodule
[OK] submodule installed
```

### LIST INSTALLED MODULES

```
$ gmm ls
[INFO] listing (/Users/paolofragomeni/workroot/0x00a/gmm)

[INFO] 📦  packager@master in ./modules/voltraco/packager
[INFO] 📦  compressor@0.1.0 in ./modules/voltraco/compressor

[OK] found 2 module(s) in gmm
```

