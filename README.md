# WG21: ${PAPER_TITLE}

This repo is a template used for making repos for creating papers for `WG21: C++ Standards Committee Papers`. Please remove this line after cloning the template.

This repo is work for [WG21: C++ Standards Committee Papers](https://www.open-std.org/jtc1/sc22/wg21/docs/papers/).


## Introduction
The top-level of this repository contains the source code for various proposals and the generated/ directory contains the generated proposals (HTML or PDF).

This repository also includes a paper-writing framework using Pandoc.

Template: [https://github.com/mpark/wg21](https://github.com/mpark/wg21).


## Published Revisions

* ${PAPER_REVISION}:
  * [https://wg21.link/${PAPER_REVISION}](https://wg21.link/${PAPER_REVISION}), ${DATE}
  * souce: [${PAPER_REVISION}.md](./revisions/${PAPER_REVISION}.md)

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
