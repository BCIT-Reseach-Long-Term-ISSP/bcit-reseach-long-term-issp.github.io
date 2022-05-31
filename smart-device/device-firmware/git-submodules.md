---
layout: default
title: Git Submodules
has_children: false
permalink: /docs/firmware/git-submodules
parent: Device Firmware
grand_parent: Smart Device
has_toc: false
nav_order: 2
---

Basics of Git Submodules
========================

This project uses git submodules for managing dependencies. To help with troubleshooting, this article will go over basics on how git commits work, then how the submodule system works.

Commits inside of git are laid out in a tree with many branches. Each and every commit is stored within a hidden directory called ".git" within the repository. When working on code, you are operating within the "working tree", which entails everything else in the repository besides the ".git" directory. Using the "git checkout" command, the working tree can be made to reflect a specific commit. These specific commits are identified by their "hash" value which is a long sequence of alphanumeric characters.

Git submodules are a way to nest git repositories within eachother. Each one operates mostly independently. All that a parent repository knows is what commit a submodule is supposed to be checked out as, and where to clone it from. When making a change to a submodule, the changes within it must first be committed and pushed to github before the parent repository can safely refer to the new commit. 

After pushing the change to the submodule itself, your local copy must first be checked out to the new commit. Once checked out, the parent repository should show that the submodule has changed. If you look at the diff, there should be two hash values corresponding to the commit: one for the commit which the repository was originally pointing at, and another for the commit that is currently checked out. Once staged and committed, the parent repository will now point to the new commit.

The git command has some utilities for working with submodules:

- `git submodule init` gets the submodules ready for checking out
- `git submodule update` clones and checks out submodules to their correct commit
- `git submodule add <repository> <path>` adds a new submodule

# Moving Submodules
One note about moving submodules, due to the fact there is configuration  inside of ".git" which needs to be updated when submodules are moved, it is recommened to *always* use the `git mv` command to move submodules.
