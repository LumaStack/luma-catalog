---
type: document
title: Why a headquarters
description: What an internal organization repository is for, why it is recommended rather than required, and what would show it was the wrong idea. Read when deciding whether to have one.
---

# Why a headquarters

**Read this when deciding whether to have one**, or arguing with how this bundle
says to run it. Somebody creating or checking a headquarters needs
[[what-a-headquarters-holds]] and a procedure, and nothing here.

## The problem it solves

**Some decisions outlive the project that prompted it.**

*We do not use that vendor.* *Every service exposes health at `/healthz`.* *That
team owns authentication and nobody else touches it.* Each of those gets decided
once, in whichever repository happened to raise it, and then binds four others
that cannot see it.

Without somewhere to put them, three things happen and all three are quiet.
**The same argument is had twice**, months apart, by people who do not know it
was settled. **A decision is lost** when the project holding it is archived.
**A project violates a rule** it had no way to read.

## Why a repository, rather than a wiki or a document

**It is the same substrate as the work.** Decisions get pull requests, reviews,
blame and history — so *when did we decide this, and who argued against it* is
answerable a year later, which is exactly when it is asked.

**It travels the same way.** An organization's catalog lives here, and a bundle
promoted from a project to the organization is a directory copy rather than an
export.

**And it stays put.** A wiki decays because nothing forces anyone past it; a
repository is where people already are.

## Why private, and why that is not negotiable

A headquarters accumulates exactly what should not be published — vendors,
internal service names, which projects are struggling, what was concluded about
a competitor, who argued for what.

**None of it is a secret a scanner would catch.** No credential, no key, nothing
a tool will flag. **That is what makes it dangerous**: the automated guard that
protects a project from publishing a token does not exist for this, so the only
protection is a rule somebody keeps.

And **publishing is not reversible.** Flipping visibility back leaves every fork,
clone, mirror and cache holding what it took. It is the leaked-credential
argument with no rotation available.

## Why recommended rather than required

**An organization with one project does not need one**, and neither does one
whose policies fit comfortably in a single `.luma/`. Creating a headquarters
before there is cross-project reasoning to put in it produces an empty
repository that makes the practice look like ceremony.

**The signal is the second occurrence**: the same argument had twice in two
repositories, or a decision in one project that quietly binds another. Until
then the nearest home is the right one, which is the same rule that governs
where a bundle belongs.

**Mandating it would also be dishonest here.** Nothing in this catalog has an
adopter, and a mandate is an assertion of authority over projects that have
never agreed to it.

## What would show this was wrong

**If headquarters go stale**, the repository is the wrong substrate — people
went where the work was and this was not it. The evidence would be a
headquarters whose last commit predates decisions everybody knows were made.

**If the boundary cannot be held**, the split is wrong. Every promotion that has
to delete the useful part in order to go upstream is a case where *general* and
*yours* were not actually separable.

**If nobody reads it**, then having somewhere to put decisions was never the
problem, and what is missing is whatever would make somebody look.
