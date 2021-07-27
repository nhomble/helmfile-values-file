repro
=====

All commands are executed such that
```bash
$ ls
helmfiles README.md
```


## Relative to CWD
Following the [overview](https://github.com/roboll/helmfile/blob/master/PATHS.md), I defined the following 'root' helmfile with paths relative to the project root.
```yml
helmfiles:
  - path: ./helmfiles/nested.yml
    values:
      - ./helmfiles/values.yml
```

then when I run the command, I an error that the values.yml doesn't exist

```bash
$ helmfile --file helmfiles/manifest.yml lint 
in helmfiles/manifest.yml: in .helmfiles[0]: in ./nested.yml: environment values file matching "./helmfiles/values.yml" does not exist in "/home/nhomble/helmfile-values-file/helmfiles/helmfiles"
```

but I can `cat` the file like you would expect from the CWD

```bash
$ cat helmfiles/values.yml
nameOverride: overriding-for-repro
```
