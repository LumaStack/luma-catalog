---
type: policy
title: The mechanical floor
description: The Go rules a linter enforces, wired into the check script so they never reach an agent's context — and which guideline each one is standing in for.
matches:
  - topic: setting up or changing Go linting, formatting, or the check script
  - path: .golangci.yml
  - path: scripts/check
---

# The mechanical floor

**A rule a linter checks does not belong in an agent's context.** It belongs in
`scripts/check`, where it fires on every change whether or not anybody
remembered it, and where it costs nothing to read.

That is not a small slice. Of the thirty-one rules in Go Code Review Comments,
roughly **seventeen are mechanically checkable** — gofmt, error strings,
initialisms, mixed caps, indent-error-flow, receiver names, blank and dot
imports, naked returns, unchecked errors, copied locks, crypto/rand, import
grouping. Of Uber's guide, about **7,700 tokens** of the 21,800 are rules a
linter already knows. Wiring them up is the single cheapest thing this bundle
asks for, and it is what makes the rest of [[writing-go]] affordable: what is
left over is the half that needs judgment.

## What `go vet` already gives you, free

`go vet` ships with the toolchain and needs no configuration. It is the floor
beneath the floor, and a project running nothing else should still run this:

```sh
go vet ./...
```

It catches copied locks, `printf` format mismatches, unreachable code, struct
tag errors, lost `context` cancels, and mistakes in `sync/atomic` alignment.
Several of these are Code Review Comments rules — *Copying*, *Format Strings
outside Printf* — enforced with nothing installed.

## The check script

**Continuous integration runs the script rather than its own copy of the
commands**, so the two cannot drift and adding a check adds it to CI.

```sh
#!/bin/sh
# Everything that must pass before a change lands.
set -e

root=$(CDPATH='' cd -- "$(dirname -- "$0")/.." && pwd)
cd "$root"

run() {
	printf '\n==> %s\n' "$*"
	"$@"
}

run go build ./...
run go vet ./...
run go test ./...
run golangci-lint run

# gofmt reports rather than fails, so the exit status has to be built here.
printf '\n==> gofmt -l .\n'
unformatted=$(gofmt -l .)
if [ -n "$unformatted" ]; then
	echo "$unformatted"
	echo "not gofmt-clean --- run: gofmt -w ." >&2
	exit 1
fi

printf '\nall checks passed\n'
```

**`gofmt -l` is the one that needs the wrapper.** It reports offending files on
stdout and exits zero either way, so a naive `run gofmt -l .` passes while
printing the problem.

## `.golangci.yml`

Written for **golangci-lint v2**, which is a different schema from v1: it needs
`version: "2"`, it takes `linters.default` rather than `disable-all`, and
formatters moved into their own block. `gosimple` and `stylecheck` no longer
exist as separate linters — both were folded into `staticcheck`.

```yaml
version: "2"

linters:
  default: standard   # errcheck, govet, ineffassign, staticcheck, unused
  enable:
    # correctness — bugs, not style
    - bodyclose
    - contextcheck
    - durationcheck
    - errorlint
    - forcetypeassert
    - makezero
    - nilerr
    - noctx
    - recvcheck
    # the style rules the guides actually name
    - errname
    - godot
    - misspell
    - nakedret
    - predeclared
    - revive
    - unconvert
    - unparam
    # modern-Go migrations the older guides predate
    - copyloopvar
    - exptostd
    - intrange
    - usestdlibvars
    - usetesting
    # security
    - gosec
    # tests
    - testifylint
    - thelper
    - tparallel

formatters:
  enable:
    - gofmt
    - goimports
```

**`revive` is doing most of the work in that list.** Its default rule set is
the old `golint` set, which is where a dozen Code Review Comments rules live:
`var-naming` (initialisms and mixed caps), `receiver-naming`,
`indent-error-flow`, `blank-imports`, `dot-imports`, `package-comments`,
`exported`, `context-as-argument`, `error-return`, `error-strings`,
`error-naming`, `errorf`, `unexported-return`, `redefines-builtin-id`.

## What is deliberately not in that list

**`gochecknoglobals` and `gochecknoinits`.** Uber's guide argues for both and
the argument is good, but a Cobra-based command line is built out of package-level
command variables and `init()` functions that register subcommands. Turning
these on there produces dozens of findings that all have the same answer.
**Enable them in a project whose shape suits them; do not inherit them by
default.**

**`wrapcheck`, `err113`, `exhaustruct`, `ireturn`, `varnamelen`, `nonamedreturns`,
`lll`, `nestif`, `funlen`, `cyclop`, `dupl`.** Each encodes a position the
guides genuinely disagree about, or a threshold somebody picked. Turning them on
is a decision to record, not a default to inherit — Go has no official line
length, `ireturn` contradicts *accept interfaces, return structs* about as often
as it supports it, and `err113` forbids a pattern the standard library uses.

**`prealloc`, `perfsprint`, `musttag`.** Fine linters, and each fires on real
issues. They are omitted only because a starting configuration that produces
findings on day one gets disabled on day two. Add them once the list above is
green.

**`rowserrcheck` and `sqlclosecheck`** matter only with `database/sql`. Add them
if you use it.

## Formatting is not negotiable and not configurable

**`gofmt` settles every mechanical style question, and there is nothing to
discuss.** That is the point of it, and it is the first line of Code Review
Comments. `goimports` is a superset that also fixes the import block.

`gofumpt` is stricter than `gofmt` and its extra rules are reasonable, but it
is a stricter-than-standard choice: adopt it deliberately or not at all, and
record it if you do.

## Getting the tools

```sh
go install github.com/golangci/golangci-lint/v2/cmd/golangci-lint@latest
```

**Pin the version in CI.** `@latest` means a new release can fail a build that
touched nothing, which teaches everybody to ignore the linter.

## The boundary

**This policy owns the check script's Go checks, not the check script.** Where a
project's `scripts/check` also runs a documentation build, a schema validation
or a spell check, those belong to whatever bundle put them there. Adding Go
linting to an existing script is adding lines, never replacing it.
