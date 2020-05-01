# Meeus

Selected algorithms from the book "Astronomical Algorithms"
by Jean Meeus, following the second edition, copyright 1998,
with corrections as of August 10, 2009.

## Repository organization

The branch "master" has the current version.  Tags exist with "semantic
versions" with a three-part major.minor.fix format like `v3.0.0`.  Older
versions can be checked out by tag.  Also a branch or branches should exist
for older versions.

Beginning with v3.0.0, code will be organized as a vgo "module" in a
subdirectory, named like `v3` corresponding to the current major version.

## Package organization

Algorithms are implemented
in subdirectories under meeus, one for each chapter of the book.  In addition
there is a package "base" with additional functions that may not be described
in the book but are useful with multiple other packages.

See meeus package documentation for a chapter title cross-reference.

## Install

### VSOP87

Routines of the `planetposition` package require "VSOP87" data files.  These
files should be available from public sources, for example
[VisieR](http://cdsarc.u-strasbg.fr/viz-bin/qcat?VI/81/).  The files needed
by planetposition are the VSOP87 "B" files.  It is sufficient to download
the eight files

    VSOP87B.ear  VSOP87B.mar  VSOP87B.nep  VSOP87B.ura
    VSOP87B.jup  VSOP87B.mer  VSOP87B.sat  VSOP87B.ven

There are no requirements on where you place these files in your file system
but you may find it convenient to create a directory for them and set an
environment variable `VSOP87` to this directory.

### Install package software with go get

Technically, `go get github.com/soniakeys/meeus/...` is sufficient.

The tests also require the sexagesimal package, so use the -t option to prompt
`go get` to find it as a test dependency:

    go get -t github.com/soniakeys/meeus/...

### Tests

With all eight VSOP87 files dowloaded as described above, and with an
environment variable set to their location, then from the meeus directory

    go test ./...

works as usual to run all tests in all subdirectories of meeus.

To run all tests except for those requiring planet positions computed from
the VSOP87 files, use

    go test -tags nopp ./...

("nopp" for no planet positions)

### Vgo

Experimentally, you can try [vgo](https://research.swtch.com/vgo).

To run package tests, clone the repository -- anywhere! it doesn't have to
be under GOPATH -- and from the cloned directory run

    vgo test all

Vgo will fetch the sexagesimal test dependency as needed and run all
package tests.

## Copyright and license

All software in this repository is copyright Shawn Lauzon and licensed with the
MIT license.

