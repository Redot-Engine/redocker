# Contribute

## Project Direction an Goal

This Project is of Technical Nature.

It is not expected to give Simple tools for Users who don't know Docker,
for use in their CI, for this [Reactions]() (will) exists.

This Project has it as a Goal to not break any Licenses.

This Project has it as a Goal to provide Single-Targeted Docker Images,
on which other Tools can build, because of the size of:

- The Redot Binary
- The Export Templates
- The Dependencies

## Progress and Flow

New Features and Tasks will first need some Discussion,
before they can be Ready to be worked on. This state is called "RFC" (Request for Comment)

An Issue might be Blocked by Temporarily by something else.
For example, if we want to do Redot X builds, we first need to wait for Readot X to provide binaries.

An Issue might also be Blocked because of License Concerns
and all work on it should be stopped till those concerns are lifted.
An Example would be MacOS and Android builds, which require the `xcode` binary and the `Android SDK`,
which according to their Licenses we can't Redistribute
(even if it is just in our Docker Images).

A License Concern might be lifted by the Core people of Redot or by a Person of Trust of the Project which is in question.

## Terminalogy

You might here some Terminalogy which you are unknown with when trying to Contribute.

- **LGTM** means "Looks Good to Me"
- **Nack** is short for "Negative Acknowoldgement", basicly a Person blocking an Issue from Moving Forward

## Nacking

A Nack should only happen by Core Members of the Project and allways requires a Technical Reason like:

- Maintainability
- Licensing Problem
- Bugs

or simmilar.
