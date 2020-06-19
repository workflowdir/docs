---
title: Fetching and scaling images
parent: Tutorials
tags:
- tutorial
---

WorkflowDir can be used to create a multi-stage workflow. For
instance, fetching images, scaling them, then placing in disparate
target locations.

In this tutorial, we'll create a workflow that downloads images from
unsplash.com, creates a resized version for the desktop as well as one
for mobile, then places them in target locations on disk.

## Create workflow definition

First, let's create the workflow definition. We'll start in a new
directory:

```sh
mkdir -p ~/my/working/directory/fetch-and-scale
pushd ~/my/working/directory/fetch-and-scale
```

Next, open a file in `~/my/working/directory/fetch-and-scale` called
`workflowdir.toml`. We'll add the following contents:

```toml
name = "Fetch and resize"

[stages]

  # input is where things always start.
  # here we specify that the output goes to the "dispatch" stage
  [stages.input]
  output = ['stages.dispatch']
  
  # the dispatch stage is a bit contrived.
  # we're using it to send files to 2 locations on down the pipeline
  [stages.dispatch]
  output = ['stages.phone', 'stages.desktop']
  
  [stages.phone]
  output = "~/Desktop/phone"
  
  [stages.desktop]
  output = "~/Pictures/background"
```

## Initialize directory structure

Now that the workflow definition is defined, we'll use `wfd` to create
the folder structure.

```sh
wfd init
```

Now you'll see that inside `~/my/working/directory/fetch-and-scale`,
we have the following contents:

```
.
├── desktop
│   └── run
├── dispatch
│   └── run
├── input
│   └── run
├── phone
│   └── run
└── workflowdir.toml

4 directories, 5 files
```

## Define discrete tasks


### input

The job of the input stage is to take URLs for images hosted on
unsplash and to download them.

For example, a sample input might be a file containing only this text:

```
https://unsplash.com/photos/QGIYdjCi0jM
```

In order to download this image, we will use `curl` to download. Then,
we'll write the contents to a unique filename given to us by `uuidgen`.

```sh
#!/bin/bash
set -uex

URL=$(cat ${1})

curl -L ${URL}/download > ${DESTINATION}/$(uuidgen).jpg
```

> *Thought:*
> do we want to generate names for items? Maybe create directories for
> each entity so that we can name it what we like?

### dispatch

Dispatch just copies the input to multiple outputs.
```sh
#!/bin/bash
set -uex

cp -v ${1} ${DESTINATION0}
cp -v ${1} ${DESTINATION1}
```

> *Thought:*
> A little contrived, and maybe not that easy to represent
> with our current schema.


### phone

Now just resize this for use on a phone.

```sh
#!/bin/bash
set -uex

convert ${1} -resize '1024x1024>' ${DESTINATION}
```

### desktop

Similarly, let's make a larger one for use on the desktop.

```sh
#!/bin/bash
set -uex

convert ${1} -resize '4096x4096>' ${DESTINATION}
```
