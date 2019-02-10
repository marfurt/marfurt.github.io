---
layout: docs
title: Xcode Tips
description: Learn about useful Xcode tips
group: mobile
lang: en
---

## Opening Xcode

Open an Xcode Workspace or Project from the Terminal:

	$ xed .

## Generated interfaces

If you're looking at a Swift data type and just want a summary of what it does, press `⌃⌘↑` to have Xcode generate an interface showing its external methods and properties.

## Running a Subset of Tests

You can run a subset of tests by pressing `⌃⌥⌘G` to re-run only your last test, or ⌘-click several tests to run only them.

## Find in Project

After using the Open Quickly shortcut `⇧⌘O` to jump to a file, type, or method in your project, use `⇧⌘J` to reveal that file in the project navigator.

## Filtering the Jump Bar

Press `⌃6` to bring up the jump bar and start typing a few letters to filter all your properties and methods using a fuzzy search.

## Focused Navigation

When you’re using the assistant editor, Xcode opens files in the primary editor by default. If you’d rather use your selected editor, activate `Uses Focused Editor` in Settings instead – files will now open in whichever editor is active.

## Multiple Selectors

Hold down Option and drag over a column of text to make edits in multiple places at the same time. Ctrl+Shift+Click lets you place new cursors at specific points.

## Measuring Build Time

Use the following command in Terminal to measure how long it takes for Xcode to build a project: 

	$ defaults write com.apple.dt.Xcode ShowBuildOperationDuration -bool YES

## Remove Old Simulators

Run `xcrun simctl delete unavailable` to remove any old simulators that are no longer supported.

## Links

- [Xcode in 20"](https://www.youtube.com/playlist?list=PLuoeXyslFTuYQ9Hoh42Bw8sPYMlTOV0V7)