---
title: Automatically resizing images
parent: Tutorials
tags:
- tutorial
---

Let's get started by building a simple workflow to resize images for a
hypothetical website.

Our hypothetical website has one requirement: no image may be larger
than 1024px in any direction. To accomplish this we are going to drop
images in `~/Desktop/LargeImages`, and we're going to expect to see
resized images in `~/Desktop/NeatlySizedImages` in no time at all.

### Install workflowdir

link to docs

### Create our target directory

This directory will be the "drop" location for any image needing resizing.

    mkdir -p ~/Desktop/LargeImages

### Initialize the directory

Let's get up and running with `wfd`:

    pushd ~/Desktop/LargeImages
    wfd init

### Create our resize action

We'll use `imagemagick` to resize the image. Run `which convert` to
see if you already have it installed. If not, `brew install
imagemagick` might just do the trick.

After confirming `convert` is available, we need to create a shell
script called `run` with the following contents:

    #!/bin/bash
    set -uex
    
    convert ${1} -resize '1024x1024>' ~/Desktop/NeatlySizedImages/${1}

### Sit back and enjoy neatly resized images

Now drop a large image in `~/Desktop/LargeImages` and wait a moment.
Pretty soon, you should see it disappear, and you'll find a smaller
version in `~/Desktop/NeatlySizedImages`. You're welcome.
