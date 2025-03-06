# wolfi-rdep-testing

Script for reverse-dependency retesting. Useful when working on a new version of something in a PR (using its presubmit repository) and you'd like to see if the new packages will not regress existing packages.

Requires a modified apkrane for full support of private repos: https://github.com/jonjohnsonjr/apkrane/pull/2

## Usage

For example, to run rests of all reverse-dependencies of the `xz` package in enterprise-packages (requires auth token to use) using the selected presubmit apk repository:

```
cd enterprise-packages/
HTTP_AUTH="basic:apk.cgr.dev:user:$(chainctl auth token --audience apk.cgr.dev)" rdep-retest \
    -i enterprise
    -S state/
    -r https://apk.cgr.dev/wolfi-presubmit/dd7308e22120f4c5b6cb7700bb72410a58d1a164 \
    xz
```

Or testing all reverse-dependencies of the libc.so.6 library (glibc) from wolfi using the selected presubmit apk repository:

```
cd os/
rdep-retest \
    -i os
    -S state/
    -L logs/
    -r https://apk.cgr.dev/wolfi-presubmit/dd7308e22120f4c5b6cb7700bb72410a58d1a164 \
    so:libc.so.6
```
