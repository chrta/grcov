# grcov

[![Build Status](https://travis-ci.org/mozilla/grcov.svg?branch=master)](https://travis-ci.org/mozilla/grcov)
[![Build status](https://ci.appveyor.com/api/projects/status/1957u00h26alxey2/branch/master?svg=true)](https://ci.appveyor.com/project/marco-c/grcov)
[![codecov](https://codecov.io/gh/mozilla/grcov/branch/master/graph/badge.svg)](https://codecov.io/gh/mozilla/grcov)

grcov collects and aggregates code coverage information for multiple source files.

This is a project initiated by Mozilla to gather code coverage results on Firefox.

## Usage

1. Download grcov from https://github.com/mozilla/grcov/releases or run ```cargo install grcov```
2. Run grcov:

```
Usage: grcov DIRECTORY_OR_ZIP_FILE[...] [-t OUTPUT_TYPE] [-s SOURCE_ROOT] [-p PREFIX_PATH] [--token COVERALLS_REPO_TOKEN] [--commit-sha COVERALLS_COMMIT_SHA] [--keep-global-includes] [--ignore-not-existing] [--ignore-dir DIRECTORY] [--llvm] [--path-mapping PATH_MAPPING_FILE] [--branch] [--filter] [--add-prefix ADDED_PREFIX_PATH]
You can specify one or more directories, separated by a space.
OUTPUT_TYPE can be one of:
 - (DEFAULT) ade for the ActiveData-ETL specific format;
 - lcov for the lcov INFO format;
 - coveralls for the Coveralls specific format.
 - coveralls+ for the Coveralls specific format with function information.
SOURCE_ROOT is the root directory of the source files.
PREFIX_PATH is a prefix to remove from the paths (e.g. if grcov is run on a different machine than the one that generated the code coverage information).
ADDED_PREFIX_PATH is a prefix to add to the paths.
COVERALLS_REPO_TOKEN is the repository token from Coveralls, required for the 'coveralls' and 'coveralls+' format.
COVERALLS_COMMIT_SHA is the SHA of the commit used to generate the code coverage data.
By default global includes are ignored. Use --keep-global-includes to keep them.
By default source files that can't be found on the disk are not ignored. Use --ignore-not-existing to ignore them.
The --llvm option must be used when the code coverage information is coming from a llvm build.
The --ignore-dir option can be used to ignore directories.
The --branch option enables parsing branch coverage information.
The --filter option allows filtering out covered/uncovered files. Use 'covered' to only return covered files, 'uncovered' to only return uncovered files.
```

Let's see a few examples, assuming the source directory is `~/Documents/mozilla-central` and the build directory is `~/Documents/mozilla-central/build`.

### LCOV output

```sh
grcov ~/Documents/mozilla-central/build -t lcov > lcov.info
```

As the LCOV output is compatible with `lcov`, `genhtml` can be used to generate a HTML summary of the code coverage:
```sh
genhtml -o report/ --show-details --highlight --ignore-errors source --legend lcov.info
```

### Coveralls/Codecov output

```sh
grcov ~/Documents/FD/mozilla-central/build -t coveralls -s ~/Documents/FD/mozilla-central --token YOUR_COVERALLS_TOKEN > coveralls.json
```

## Build & Test

```
cargo build
```

To run tests:
```
cargo test
```

## Minimum requirements

- GCC 4.9 or higher is required (if parsing coverage artifacts generated by GCC).

## License

Published under the MPL 2.0 license.
