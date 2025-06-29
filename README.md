# WG21 P3022: A Boring Thread Attributes Interface

Authors: Darius Neațu ([@neatudarius](https://github.com/neatudarius)), David Sankel ([@camio](https://github.com/camio))

Audience: Library Evolution

Description: The standard library lacks facilities to configure stack sizes or names for threads. This has resulted in a proliferation of code making use of unportable, platform-specific thread libraries. This paper argues that a simple, standardized, thread attribute API is a preferred solution to this problem.

> Note: This repo/paper is work for [WG21: C++ Standards Committee Papers](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/).

## Introduction
The top-level of this repository contains the source code for various proposals and the generated/ directory contains the generated proposals (HTML or PDF).

This repository also includes a paper-writing framework using Pandoc.

Template: [https://github.com/mpark/wg21](https://github.com/mpark/wg21).


## Published Revisions

* P3022R0:
  * [https://wg21.link/P3022R0](https://wg21.link/P3022R0), 2023-10-14.
  * source: [P3022R0.md](./revisions/P3022R0.md)
 
* P3022R1:
  * [https://wg21.link/P3022R1](https://wg21.link/P3022R1), 2023-11-28.
  * source: [P3022R1.md](./revisions/P3022R1.md)

Resolution: [cplusplus: P3022 R1 A Boring Thread Attributes Interface #1683
](https://github.com/cplusplus/papers/issues/1683) was closed with P3022 being rejected. Details in `LEWG feedback section` from `P3022R1`.

## Install Deps

```bash
# actual install
$ deps/install.sh

# optional extra git hooks activation
$ cd .git/hooks && ln -fs ../../.hooks/pre-push . && cd -
```

## Export Papers

```bash
$ make <paper>.pdf  # `<paper>.md` -> `generated/<paper>.pdf`
$ make <paper>.html # `<paper>.md` -> `generated/<paper>.html`
```

## Run Linters

Linters are automatically run at `git push`. Check:
```bash
$ cat .git/hooks/pre-push | grep hooks
"${REPO_PATH}/.hooks/lint-bash.sh" -r "${REPO_PATH}"
"${REPO_PATH}/.hooks/lint-cpp.sh" -r "${REPO_PATH}"
```

### clang-format
```bash
$ .hooks/lint-cpp.sh -h  
usage: run-clang-format.py [-h] [--clang-format-executable EXECUTABLE] [--extensions EXTENSIONS] [-r] [-d] [-i] [-q] [-j N] [--color {auto,always,never}] [-e PATTERN] [--style STYLE] file [file ...]

A wrapper script around clang-format, suitable for linting multiple files and to use for continuous integration. This is an alternative API for the clang-format command line. It runs over multiple files and directories in parallel. A diff
output is produced and a sensible exit code is returned.

positional arguments:
  file

optional arguments:
  -h, --help            show this help message and exit
  --clang-format-executable EXECUTABLE
                        path to the clang-format executable
  --extensions EXTENSIONS
                        comma separated list of file extensions (default: c,h,C,H,cpp,hpp,cc,hh,c++,h++,cxx,hxx)
  -r, --recursive       run recursively over directories
  -d, --dry-run         just print the list of files
  -i, --in-place        format file instead of printing differences
  -q, --quiet           disable output, useful for the exit code
  -j N                  run N clang-format jobs in parallel (default number of cpus + 1)
  --color {auto,always,never}
                        show colored diff (default: auto)
  -e PATTERN, --exclude PATTERN
                        exclude paths matching the given glob-like pattern(s) from recursive search
  --style STYLE         formatting style to apply (LLVM, Google, Chromium, Mozilla, WebKit)

# dry-run auto check for changes
$ .hooks/lint-cpp.sh -r .
--- ./src/main.cpp	(original)
+++ ./src/main.cpp	(reformatted)
@@ -1,7 +1,4 @@
 int main() {
-    
 
-
-
-    // bad format example
+  // bad format example
 }% 

# in-place auto changes
$ .hooks/lint-cpp.sh -r . -i
```

### shellcheck

```bash
$ .hooks/lint-bash.sh -h 
Usage: .hooks/lint-bash.sh [-h] -r 

Example: .hooks/lint-bash.sh -r .
```
