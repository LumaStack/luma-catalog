---
type: policy
title: Writing Go
description: The Go guidelines this project writes against, which one wins when they disagree, and how to read them without spending a context window.
matches: eager
---

# Writing Go

## Step zero: keep local copies

**Cache them, and read the copies.**

```
~/.cache/luma/luma-foreman/bundles/lumastack/luma-catalog/go-guidelines/
  effective-go.html
  code-review-comments.md
  test-comments.md
  google-style-guide.md
  google-style-decisions.md
  google-best-practices.md
  uber-style.md
```

**Fetch the sources, not the rendered pages.** Every one of these has a
plain source behind a styled site, and the source greps well:

```
curl -sSL -o ~/.cache/luma/luma-foreman/bundles/lumastack/luma-catalog/go-guidelines/effective-go.html \
  https://raw.githubusercontent.com/golang/website/master/_content/doc/effective_go.html
curl -sSL -o ~/.cache/luma/luma-foreman/bundles/lumastack/luma-catalog/go-guidelines/code-review-comments.md \
  https://raw.githubusercontent.com/golang/wiki/master/CodeReviewComments.md
curl -sSL -o ~/.cache/luma/luma-foreman/bundles/lumastack/luma-catalog/go-guidelines/test-comments.md \
  https://raw.githubusercontent.com/golang/wiki/master/TestComments.md
curl -sSL -o ~/.cache/luma/luma-foreman/bundles/lumastack/luma-catalog/go-guidelines/google-style-guide.md \
  https://raw.githubusercontent.com/google/styleguide/gh-pages/go/guide.md
curl -sSL -o ~/.cache/luma/luma-foreman/bundles/lumastack/luma-catalog/go-guidelines/google-style-decisions.md \
  https://raw.githubusercontent.com/google/styleguide/gh-pages/go/decisions.md
curl -sSL -o ~/.cache/luma/luma-foreman/bundles/lumastack/luma-catalog/go-guidelines/google-best-practices.md \
  https://raw.githubusercontent.com/google/styleguide/gh-pages/go/best-practices.md
curl -sSL -o ~/.cache/luma/luma-foreman/bundles/lumastack/luma-catalog/go-guidelines/uber-style.md \
  https://raw.githubusercontent.com/uber-go/guide/master/style.md
```

**Fetch to the file, never through the context window.** `curl -o <path>`
puts the bytes on disk at no token cost; fetching one *into* a reply spends
the whole document in order to save it. Write the date fetched and the source
URL as the first line of each file, so nothing can read the content without
seeing how old it is.

**Refresh when the recorded date is not today, and only then.** That is
"once per session" expressed as something a reader can check — an agent has no
memory of what it did earlier in the session, but it can compare a date. Never
block on it: if there is no network or a fetch fails, use what is cached and
say how old it is.

**Never commit them.** These are machine-local. Four of the seven are
Creative Commons and one is Apache-2.0, and a copy on one machine is nobody's
business while a copy in a published repository is distribution that carries
the licence with it. That is the whole reason this bundle points rather than
carries — see the manifest.

## Step one: the mechanical floor comes first

**Before reading a word of guidance, make the tools enforce what tools can
enforce.** See [[mechanical-floor]]. Roughly half of what these documents say
is checkable by a linter, and a rule a linter checks does not belong in an
agent's context at all — it belongs in `scripts/check`, where it fires on
every change without anybody remembering it.

Everything below is about the other half: the decisions no linter makes.

## Step two: which document, and in what order

**These four disagree with each other, and the disagreements are real** —
naked returns, receiver naming, when to wrap an error, whether to define an
error type at all. Somebody has to rank them, so this bundle does.

### 1. Google's Go Style Guide — the modern centre

<https://google.github.io/styleguide/go/guide> — and its two longer companions,
[Style Decisions](https://google.github.io/styleguide/go/decisions) and
[Best Practices](https://google.github.io/styleguide/go/best-practices).

**The most current comprehensive treatment, and the one the others defer to.**
Start here for anything the checklist below does not settle. It is also by far
the largest — about 71,000 tokens across the three — so it is read by seeking,
never whole.

Its own ordering is worth keeping: the *Style Guide* is the short statement of
principle, *Style Decisions* is the ruling on specific questions, and *Best
Practices* is the long-form advice. Ask them in that order.

### 2. Go Code Review Comments — the fast checklist

<https://go.dev/wiki/CodeReviewComments>

**Thirty-one named rules in about 6,000 tokens, and the best value per token
in the whole set.** It is what the Go core team looks for in review, and it is
short enough to read whole.

**It describes itself as "a laundry list of common style issues, not a
comprehensive style guide" and points at Google's as the longer treatment** —
which is why it sits second here rather than first. Where the two disagree,
Google's is newer.

Its companion for tests is [Go Test Comments](https://go.dev/wiki/TestComments).

### 3. Effective Go — foundational, and frozen

<https://go.dev/doc/effective_go>

**Read it once, for how Go thinks.** It is where the language's own idea of
itself is written down, and nothing has replaced it for that.

**It carries an upstream staleness notice and the notice is not decorative:**

> This document was written for Go's release in 2009 and is not actively
> updated. While it remains a good guide for using the core language, it does
> not cover significant changes to the language (generics), ecosystem
> (modules), or libraries added since.

So it is authoritative about idiom and silent about half of modern Go. **Never
resolve a question about generics, modules, error wrapping, or anything added
after 2009 from this document** — its silence is absence of coverage, not a
position. Where it and a newer source appear to conflict, the newer source
wins by default.

### 4. Uber's Go Style Guide — pragmatic, and house style

<https://github.com/uber-go/guide/blob/master/style.md>

**Worth reading for the parts nobody else covers**: goroutine lifetimes and
fire-and-forget, functional options, table-driven tests, embedding in public
structs, `nil` as a valid slice, and the argument for copying slices and maps
at API boundaries.

**Read it as one large codebase's house style rather than as Go's.** Some of
it is Uber convention with no standing outside Uber — prefixing unexported
globals with `_` is the clearest example. Where it contradicts Google's guide
on a question of Go-wide style, Google's wins; where it covers ground nobody
else covers, take it.

**And one section is actively out of date.** *Use `go.uber.org/atomic`* argues
for a third-party dependency to get type-safe atomics and `atomic.Bool`. Both
have been in the standard library since **Go 1.19** — `atomic.Bool`,
`atomic.Int32`, `atomic.Int64`, `atomic.Pointer[T]`. Use `sync/atomic`. Do not
add the dependency.

### Go Proverbs — the tiebreaker

<https://go-proverbs.github.io> — Rob Pike's aphorisms, and the closest thing
Go has to a statement of taste. They settle nothing specific and they are
often the right answer when two specific rules both apply:

> Clear is better than clever.
> Don't communicate by sharing memory, share memory by communicating.
> A little copying is better than a little dependency.
> The bigger the interface, the weaker the abstraction.
> Make the zero value useful.
> `interface{}` says nothing.
> Errors are values.
> Don't just check errors, handle them gracefully.
> Design the architecture, name the components, document the details.
> Documentation is for users.

## Step three: how to read them

**Read Code Review Comments whole, once, in any session that will write
non-trivial Go.** Six thousand tokens for thirty-one rules is the one document
here that repays a full read, and **you cannot seek for a rule you do not know
exists** — the rules you would not have thought to look up are exactly the ones
a checklist is worth having.

**Seek in the other three.** They total about 120,000 tokens; reading them
whole is not a thing that happens, and pretending otherwise produces a policy
nobody follows. The cached copies make seeking cheap: coming back for *what
does Google say about error wrapping* costs forty lines instead of thirty
thousand.

**Read Effective Go whole once ever, not once per session.** It is background
for how the language thinks, and it does not change — it has not been updated
since 2009.

## Step four: what outranks all of it

**A decision that is in force.** Where this project has recorded a decision
about its Go and that decision is in force — `provisional` or `stable`, not
`draft` — it was made with context no external guide has, and it is the
answer. A `draft` is a proposal, so it outranks nothing, though it may be
worth mentioning.

**The standard library is evidence, not authority.** `net/http` and `os` are
full of shapes no style guide would approve today, because they predate the
guides and cannot change. Read the standard library to learn what idiomatic Go
looks like; do not cite it to justify a choice a guide rules against.

**What the codebase already does is not an argument.** Precedent is not a
decision. A convention can be established and still be wrong, and adopting
this bundle is a commitment to improving the code rather than preserving
whichever shape it drifted into.

**Follow the user's directives.** If a user gives a directive to break from
these guidelines, tell them what is being broken so they know, then follow the
directive for the rest of the session.

## Step five: record what you decided

**Where this project departs from the order above, write down why.** A
convention broken on purpose and one broken by accident look identical in the
code, and nobody can tell them apart later without a record.

**Record the choices the guides leave open, too.** Package layout beyond
`cmd/` and `internal/`, whether errors are wrapped with `%w` at every layer or
only at boundaries, how table tests name their cases, what goes in a
constructor versus an option — these are answered differently by different
guides or not at all, and a project that has not settled them will answer them
differently every time somebody adds a file.

**Until it is recorded and in force, it does not bind.** The way to make
something outrank these guides is to decide it deliberately and write it down,
not to do it twice.

## Disclaimer

**None of these documents is summarised here on purpose.** Effective Go, Code
Review Comments and Google's Style Guide are Creative Commons; Uber's is
Apache-2.0. Each carries attribution obligations that would travel into every
repository adopting this bundle, so this bundle points at them and restates
none of them. Read the sources.
