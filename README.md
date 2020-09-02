# Can the Ant task `patch` be used in Linux for patching files with DOS linefeed?

## Files

- [build.xml](build.xml): Ant build file with a patch task
- [README.md](README.md): this file
- [test.patch](test.patch): patch file with DOS linefeeds
- [test.txt](test.txt): source file with DOS linefeeds

## Command line `patch` fails

DOS linefeeds in the patch file are converted into Unix linefeeds and patching
fails:

```
[0] mypc<u0>:~/src/test/ant_patch_crlf>patch -i test.patch
(Stripping trailing CRs from patch; use --binary to disable.)
patching file test.txt
Hunk #1 FAILED at 1 (different line endings).
1 out of 1 hunk FAILED -- saving rejects to file test.txt.rej
```

## Command line `patch --binary` works fine

As suggested above

> `use --binary to disable`

adding the option `--binary` helps:

```
[0] mypc<u0>:~/src/test/ant_patch_crlf>patch --binary -i test.patch
patching file test.txt
```

## Ant task `patch` fails

Ant task `patch` fails with the same error than command line without the
option `--binary`:

```
[0] mypc<u0>:~/src/test/ant_patch_crlf>ant                              
Buildfile: /home/u0/src/test/ant_patch_crlf/build.xml

patch:
    [patch] (Stripping trailing CRs from patch; use --binary to disable.)
    [patch] patching file test.txt
    [patch] Hunk #1 FAILED at 1 (different line endings).
    [patch] 1 out of 1 hunk FAILED -- saving rejects to file test.txt.rej
    [patch] 'patch' failed with exit code 1

BUILD SUCCESSFUL
Total time: 0 seconds
```

## Ant questions

How can we...
1. use the Ant task `patch` for patching files with DOS linefeed?
2. apply `--binary` mode with the Ant task `patch`?

