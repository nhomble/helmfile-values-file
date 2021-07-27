repro
=====
**Issue raised:** https://github.com/roboll/helmfile/issues/1931

## Context
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

then when I run the command, there is an error that the values.yml doesn't exist

```bash
$ helmfile --file helmfiles/manifest.yml lint 
in helmfiles/manifest.yml: in .helmfiles[0]: in ./nested.yml: environment values file matching "./helmfiles/values.yml" does not exist in "/home/nhomble/helmfile-values-file/helmfiles/helmfiles"
```

but I can `cat` the file like you would expect from the CWD

```bash
$ cat helmfiles/values.yml
nameOverride: overriding-for-repro
```

## What works: relative to manifest (and putting values in the nested helmfile)
On this [branch](https://github.com/nhomble/helmfile-values-file/tree/move-values), I did the same test after:
- moving the `values:` into the `nested.yml`
- making all paths relative to the helmfile rather than CWD

Then it works as expected
```bash
$ helmfile --file helmfiles/manifest.yml lint
Adding repo bitnami https://charts.bitnami.com/bitnami
"bitnami" has been added to your repositories

Fetching bitnami/nginx
Linting release=repro, chart=/tmp/helmfile701780459/repro/bitnami/nginx/latest/nginx
==> Linting /tmp/helmfile701780459/repro/bitnami/nginx/latest/nginx

1 chart(s) linted, 0 chart(s) failed
```
