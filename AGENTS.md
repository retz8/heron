# AGENTS.md

Instructions for a coding agent working in this repository.

## What Heron is

A tool that follows the upstreams a project is tied to (its patched dependencies, vendored copies and waits), tells the project what changed, and keeps a record of how each change was judged. Nothing is built yet.

## Where things are

- [`_dev/docs/spec/first-version.md`](_dev/docs/spec/first-version.md) is the design authority for the first version.
- [`_dev/TODO.md`](_dev/TODO.md) holds the phases of the work.

## Building, running and testing

There is no code yet. Do not guess a command: a package's README has its build, run and test steps.

## The general frame

Heron is for any project tied to an upstream. Its first adopters are adopters, not its host: nothing in Heron names, assumes or is shaped for one adopter's upstream, repositories or workflow.

## Writing instruction files

Keep this file and Heron's skill vendor-neutral: no model names and no tool names of one assistant.
