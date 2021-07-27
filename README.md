repro
=====

All commands are executed such that
```bash
$ ls
helmfiles README.md
```


## Relative to CWD
Following the [overview](https://github.com/roboll/helmfile/blob/master/PATHS.md)

```bash
$ helmfile --file helmfiles/manifest.yml lint 
in helmfiles/manifest.yml: in .helmfiles[0]: in ./nested.yml: environment values file matching "./helmfiles/values.yml" does not exist in "/home/nhomble/helmfile-values-file/helmfiles/helmfiles"
```
